```
====================
function choose_subj
{
    set -A subjects $(command ls)
    PS3="Choose a subject for the quiz from the preceding list: "
    select Subject in $subjects; do
    if [[ -z$Subject ]]; then
        print "No subject Chosen." >&2
        exit 1
    fi
    print $Subject
    return 0
done
```

```
====================
function exchange
{
    temp_value=${questions[$1]}
    questions[$1]=${questions[$2]}
    questions[$2]=temp_value
}
```

```
====================
function scramble
{
    typeset -i index quescount
    set -A questions $(command ls)
    quescount=$#questions
    ((index=quescount-1))
    while [[ $index > 0 ]]; do
        ((target=RANDOM % index))
        exchange $target $index
        ((index -= 1))
    done
done
```

```
====================
function ask
{
    set -A choices
    exec 3<$1
    read -u3 quels || exit 2
    read -u3 num_opts || exit 2
```

```
index=0
while (( index < num_opts )); do
    read -u3 next_choice || exit 2
    choices=($choices $next_choice)
    ((index += 1))
done
```

```
read -u3 correct_answer || exit 2
exec 3<-
if [[ $first_time = true ]]; then
    first_time=false
```