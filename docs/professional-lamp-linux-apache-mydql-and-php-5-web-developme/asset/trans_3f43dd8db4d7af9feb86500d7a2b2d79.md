

-   **stream_write()**: 同样，此函数仅应在流确实可写入时调用。流对象有责任跟踪从一次写入到下一次写入之间执行的操作。你无需写入所有接收到的字节；如有必要，可以截断数据。无论如何，此方法应返回已写入的字节数（如果完全无法写入，则返回 0）。这个数字应以接收到的字节数来表示。执行 base64 编码的流将为每接收三个字节返回四个字节。如果被要求写入 "abc"，它会写入 “YWJj”，但仍返回 3。此返回值是为了方便调用者使用，因为按定义，调用者本不该深入了解“被调用者”的操作细节。如果你写入的字节数少于请求的数量，由调用者决定是否重试，但你的流无论如何可能都需要保留一些数据。base64 编码器就是这种情况的一个例子：被传入 "ab" 后，它能够写入 “YWI”，但 “b” 的最后两个位必须保留，直到流等待下一个输入字节或调用 stream_close()。此编码器应返回 1，并期望在下一次 stream_write() 调用中再次传入 “b”。另一种机制是编码器除非至少有三个字节可编码，否则不输出任何内容，并且它一次只编码（并输出）三个输入字节的倍数。为了使其正常工作，流需要声称已写入所有传入的字节，即使实际上并未做到，并希望没有人发现其这种策略。否则，调用者可能会因为传入 "ab" 时返回 0 而生气并反复尝试，而编码器却在等待第三个字节，但该字节永远不会到达。

-   **stream_eof()**: 可读流随时可能被询问流数据是否已到达末尾（特别是在 stream_read() 因某种原因返回空字符串之后）。因此，这只是一个布尔函数，如果流已到达末尾则返回 "true"。

-   **stream_close()**: 流对象有责任清理需要清理的内容，关闭其自身的任何流，等等。回到 base64 编码器，流很有可能剩余一到两个字节，这些字节将永远无法成为三元组的一部分。因此，安全做法是最终编码这些字节并写出，用相应数量的 = 符号进行填充。

这些是打开和关闭流以及读写流的基础知识。流包装器还有其他方法，如果适合协议，则应实现它们，以涵盖随机访问、目录控制等任务。

当流打开时，stream_open() 会被调用，其第一个参数是包含协议的完整路径。这主要是为了让你可以使用 parse_url() 将路径分解为各个组件，因此最好将你的流名称格式设计为在适当的地方使用传统的 URL 语法（scheme://username:password@host:port/path?query#fragment）。顺便说一句，这也意味着同一个流类可以处理多种协议，但这最好通过子类化处理。

## 流的两个示例

为了巩固上一节中的概念，这里有两个简单的流类。第一个维护一个日志文件，记录通过它访问的文件的活动，而第二个用于选择地理航空摄影集合的一部分。

## 第 3 章

### 文件访问日志记录器

考虑以下代码：

```php
<?php
class logged_stream
{
    private $stream;
    private $log_stream;
    private $bytes_read=0, $bytes_written=0;
    private $user;

    function stream_open($path, $mode, $options, &$opened_path)
    {
        static $modes = array(
            'r' => 'reading',
            'r+' => 'reading and writing',
            'w' => 'writing',
            'w+' => 'writing and reading',
            'a' => 'appending',
            'a+' => 'appending and reading',
            'x' => 'creation and writing',
            'x+' => 'creation, writing and reading');
        $path = substr($path, 9);
        $this->user = substr($path, 0, strpos($path, '@'));
        $path = substr($path, strpos($path, '@')+1);
        $this->stream = fopen($path, $mode, $options&STREAM_USE_PATH);
        $this->log_stream = fopen($path . '.log', 'a');
        if(!($this->log_stream))
        {
            if($options&STREAM_REPORT_ERRORS)
            {
                trigger_error('Logged stream: Unable to open log file',
                              E_USER_WARNING);
            }
            return false;
        }
        if(!($this->stream))
        {
            if($options&STREAM_REPORT_ERRORS)
            {
                trigger_error('Logged stream: file `$path` could not be opened',
                              E_USER_WARNING);
            }
            return false;
        }
        $binary = strpos($mode, 'b')!==false;
        if($binary)
            $mode = str_replace('b', '', $mode);
        list($micro, $sec) = explode('.', microtime());
        $date = date('Y-m-d H:i:s', substr($micro, 1));
        fwrite($this->log_stream, 'File opened for ' . $modes[$mode] . '
            ' . ($binary?" in binary mode by ':" by ") . $this->user . ' at ' . $date . "\n");
        return true;
    }

    function stream_close()
    {
        fclose($this->stream);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        fwrite($this->log_stream, 'File closed by ' . $this->user . ' at ' . $date . "\n");
        fwrite($this->log_stream, "Total bytes read: " . $this->bytes_read . "\n");
        fwrite($this->log_stream, "Total bytes written: " . $this->bytes_written . "\n");
        fwrite($this->log_stream, "\n");
        fclose($this->log_stream);
    }

    function stream_read($count)
    {
        ob_start();
        debug_print_backtrace();
        $backtrace = ob_get_clean();
        fwrite($this->log_stream, $backtrace);
        $read = fread($this->stream, $count);
        $this->bytes_read += strlen($read);
        return $read;
    }

    function stream_write($data)
    {
        $read = fwrite($this->stream, $data);
        $this->bytes_written += strlen($read);
        return $read;
    }

    function stream_eof()
    {
        return feof($this->stream);
    }

    function stream_tell()
    {
        return ftell($this->stream);
    }

    function stream_seek($offset, $whence=null)
    {
        return fseek($this->stream, $offset, $whence);
    }

    function stream_flush()
    {
        return true;
    }

    function stream_stat()
    {
        return fstat($this->stream);
    }

    function unlink($path)
    {
        $log_stream = fopen($path.'.log', 'a');
        if(!$log_stream)
        {
            trigger_error('Logged stream: Unable to open log file. File not deleted.', E_USER_WARNING);
            return false;
        }
        $success = unlink($path);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        if($success)
            fwrite($log_stream, "File $path deleted at $date\n");
        else
            fwrite($log_stream, "Unable to delete file $path at $date\n");
        fclose($this->log_stream);
        return $success;
    }

    function rename($from_path, $to_path)
    {
        $from_log_stream = fopen($from_path.'.log', 'a');
        $to_log_stream = fopen($to_path.'.log', 'a');
        if(!$from_log_stream || !$to_log_stream)
        {
            trigger_error('Logged stream: Unable to open log file. File not renamed.',
                          E_USER_WARNING);
            return false;
        }
        $success = rename($from_path, $to_path);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        if($success)
        {
            fwrite($from_log_stream, "File $from_path renamed to $to_path at $date\n");
            fwrite($to_log_stream, "File $to_path renamed from $from_path at $date\n");
        }
        else
        {
            fwrite($from_log_stream, "Unable to rename $from_path as $to_path at $date\n");
            fwrite($to_log_stream, "Unable to rename $from_path as $to_path at $date\n");
        }
        fclose($from_log_stream);
        fclose($to_log_stream);
        return $success;
    }
}
?>
```

该包装器通过调用 stream_wrapper_register('logged', 'logged_stream') 进行注册。你可以通过调用类似 $fp=fopen('logged://eric@documents/benchmarks.txt'); 的内容来使用 "logged" 流。这旨在表示用户 "eric" 将操作 documents/benchmarks.txt，并且要求记录该事件：

```php
$path = substr($path, 9);
$this->user = substr($path, 0, strpos($path, '@'));
$path = substr($path, strpos($path, '@')+1);
```

