

## 5.2.2.4 主程序

主函数初始化所有必要的内容，然后进入一个循环，保持在此循环中，直到用户在 lastline 模式下输入退出命令。下面的列表中仅显示了主循环。

### Listing 5.9: main program loop

```
while ( !quit ) {
    if ( in_input_mode ) {
        if ( read(STDIN_FILENO, &c, 1) > 0 ) {
            if ( c == ESCAPE ) {
                in_input_mode = 0;
                write_status_message( "", curs);
            }
            else {
                in_input_mode = handle_insertion(&buf, &win, &curs, c);
                if ( in_input_mode == UNHANDLEDCHAR )
                    in_input_mode = 1;
                else
                    write_status_message( INSERT, curs);
            }
        }
    }
    else {
        if ( read(STDIN_FILENO, &c, 1) > 0 ) {
            switch ( c ) {
            case 'i':
                in_input_mode = 1;
                park();
                update_buffer_index(&buf);
                moveto(curs.r, curs.c);
                write_status_message( INSERT, curs);
                break;
            case ':':
                in_lastline_mode = 1;
                park();
                write(1,&prompt, 1);
                status = do_lastline_mode( buf, win, curs);
                if ( status >= 0 ) quit = status;
                moveto(curs.r, curs.c);
                break;
            case '\003':
                write_status_message( CTRLC, curs);
                break;
            case '\004':
                write_status_message( CTRLD, curs);
                break;
            case '\010':
                write_status_message( CTRLH, curs);
                break;
            case 'j':
                moveDown(&buf, &win, &curs );
                break;
            case 'k':
                moveUp(&buf, &win, &curs );
                break;
            case 'l':
            case ',':
                moveRight(&buf, &win, &curs );
                break;
            case 'h':
                moveLeft(&buf, &win, &curs );
                break;
            case ESCAPE:
                handle_escape_char( &buf, &win, &curs );
                break;
            default:
                if ( c == win.erase_char )
                    moveLeft(&buf, &win, &curs );
            }
        }
    }
}
```

该程序包含了所有不涉及时间的交互式应用的元素。本章的其余部分将介绍 UNIX API 的特性，这些特性对于程序状态随时间变化的程序是必需的。

## 5.2.3 非阻塞输入

改变终端本身的状态比改变打开的文件描述符的属性更可取，因为这样我们可以对其进行更精细的控制。然而，其缺点是使用该终端的所有程序都会受到更改的影响。通常这不是问题，因为你编写的程序将是唯一的进程，而在它运行时不会有其他进程从终端读取。然而，了解如何通过文件描述符使用 O_NDELAY 标志（在 POSIX 中称为 O_NONBLOCK）对输入进行有限控制是值得的。

O_NONBLOCK 标志控制读写是阻塞还是非阻塞。当读取是阻塞时，执行读取的进程会等待直到输入可用，然后才继续。这是初学者程序员所学习的语义。这是有道理的；毕竟，如果读取没有产生任何数据，为什么你会希望程序继续执行读取指令之后的代码呢？

练习。在继续阅读之前，尝试回答前面的问题。

非阻塞 I/O 是打开文件连接的属性，而不是终端或设备的属性；当你打开一个文件并将 open() 调用的返回值作为文件描述符时，你可以在调用中指定文件连接应为非阻塞。换句话说，非阻塞的属性是进程与文件或终端的连接的一部分，而不是终端本身。两个不同的进程可以同时打开同一个文件进行读取，一个使用阻塞读取，另一个使用非阻塞读取。

请记住，当进程与输入源之间建立连接时，会创建一个缓冲区，用于在数据从源传输到进程的途中暂存数据。无论是磁盘文件、终端、指向设备还是音频源，都会使用某种临时存储区域来

