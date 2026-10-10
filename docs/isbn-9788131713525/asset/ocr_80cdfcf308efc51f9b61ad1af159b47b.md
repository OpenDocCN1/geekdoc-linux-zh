```
12end

13

14# State

15if ($arg0->state == 0)

16  printf "Running "

17else

18  if ($arg0->state == 1)

19    printf "Sleeping "

20  else

21    if ($arg0->state == 2)

22      printf "DiskSleep "

23    else

24      if ($arg0->state == 4)

25        printf "Zombie "

26      else

27        if ($arg0->state == 8)

28          printf "Stopped "

29        else

30          if ($arg0->state == 16)

31            printf "WPaging "

32          else

33            printf "%2d       ", $arg0->state

34          end

35        end

36      end

37    end

38  end

39

40

41# User NIP

42if ($arg0->thread_regs)

43  printf "0x%08X ", $arg0->thread_regs->nip

44else

45  printf "*"

46end

47

48# Display the kernel stack pointer

49printf "0x%08X ", $arg0->thread.ksp

50

51# device

52if ($arg0->signal->tty)

53  printf "%s  ", $arg0->signal->tty->name

54else

55  printf "(none)"

56end

57

58# comm

59printf "%s\n", $arg0->comm

60end
```