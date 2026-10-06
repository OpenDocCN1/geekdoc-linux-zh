# Buffers

Before we start editing our new file, let's look at what vim is doing. Each file that we edit is stored in a buffer. We can look the current list of buffers this way: 

```
:ls
```

This will display the list. There are several ways that we can switch buffers. The first way is to cycle between them:

```
:bn
```

This command (short for :bnext) cycles through the buffer list, wrapping around at the end. Likewise, there is a :bp (:previous) command which cycles through the buffer list backwards. We can also select a buffer by number:

```
:b 2
```

We can cycle back to our new buffer and add this line to our configuration file:

```
setlocal number
```

This will turn on line numbering each time we load a shell script. Notice that the setlocal command rather than set. This is because set will apply an option globally, whereas the setlocal command only applies the option to the current buffer. This will prevent settings conflicts when we edit multiple files of different types.

We can also control syntax highlighting while we're here. We can turn it on with:

```
syntax on
```

Or turn it off with:

```
syntax off
```

We'll save this file, now before we do, let's type mS (lowercase m uppercase S), similar to what we did when we saved our initial .vimrc.

Help topics: :ls :buffers :bnext :previous :setlocal 'number' :syntax

# Tabs

Before we leave the subject of buffers, let's take a look at possible way of using them. We have already discussed splits and windows, but recent versions of vim include a useful alternative called tabs. As the name suggests, this feature allows each buffer to appear in its own tab.

To create a new tab, we type the following command:

```
:tabnew
```