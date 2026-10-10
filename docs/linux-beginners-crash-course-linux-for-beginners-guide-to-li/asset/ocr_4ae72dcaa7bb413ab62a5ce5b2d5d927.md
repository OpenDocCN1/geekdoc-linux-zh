necessary. The second is -v, which commands mkdir to tell us what it’s doing.

Here’s an example with the -p option:

```
mkdir -p linuxtutorialwork/foo/bar
cd linuxtutorialwork/foo/bar
pwd
/home/Simon/linuxtutorialwork/foo/bar
```

Now let’s look at the same example using the -v option as well:

```
mkdir -pv linuxtutorialwork/foo/bar
mkdir: created directory 'linuxtutorialwork/foo'
mkdir: created directory 'linuxtutorialwork/foo/bar'
cd linuxtutorialwork/foo/bar
pwd
/home/Simon/linuxtutorialwork/foo/bar
```