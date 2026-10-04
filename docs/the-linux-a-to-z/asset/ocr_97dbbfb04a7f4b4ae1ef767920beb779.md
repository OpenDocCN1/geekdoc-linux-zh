```
size=`wc -c <$i`
if test $size -lt $2
then
    echo `basename $i` has size $size bytes
fi
fi
done
```