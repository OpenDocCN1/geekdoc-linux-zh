# **File Access Logger**

Consider the following code:

```
```php
<?php
class logged_stream
{
  private $stream;
  private $log_stream;
  private $bytes_read=0, $bytes_written=0;
  private $user;

function stream_open($path, $mode, $options, &fopened_path)
{

  static $modes = array(
      'r'=> ‘reading',
      'r+'=>'reading and writing',
      'w'=>‘writing',
      'w+'=>'‘writing and reading',
      'a'=>‘appending',
      'a+'=>'‘appending and reading',
      'x'=>‘creation and writing',
      'x+'=>'‘creation and reading');
  $path = substr($path, 9);
  $this->user = substr($path, 0, strpos($path, '@'));
  $path = substr($path, strpos($path, '@')+1);
  $this->stream = fopen($path, $mode, $options&STREAM_USE_PATH);
  $this->log_stream = fopen($path. '.log', 'a');
  if(!$this->log_stream)
  {
    if($options&STREAM_REPORT_ERRORS)
    {
      trigger_error('Logged stream: Unable to open log file',
                E_USER_WARNING);
    }
    return false;
  }
  if(!$this->stream)
  {
    if($options&STREAM_REPORT_ERRORS)
    {
      trigger_error('Logged stream: file ‘$path.' could not be opened',
                E_USER_WARNING);
    }
    return false;
  }
  $binary = strpos($mode, 'b')!==false;
  if($binary)
    $mode = str_replace('b', '', $mode);
  list($micro, $sec) = explode(‘.', microtime());
  $date = date('Y-m-d H:i:s').substr($micro, 1);
  fwrite($this->log_stream, 'File opened for ‘$modes[$mode]
          ($binary?' in binary mode by ':' by ').$this->user.’ at ‘.$date.“\n”);
  return true;
}
```
```