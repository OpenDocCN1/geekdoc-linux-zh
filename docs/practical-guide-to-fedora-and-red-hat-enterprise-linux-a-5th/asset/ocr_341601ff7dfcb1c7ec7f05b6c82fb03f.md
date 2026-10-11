```
```shell
###############
function exchange ()
{
temp_value=$\{questions[\$1]\}
questions[\$1]=$\{questions[\$2]\}
questions[\$2]=$temp_value
}
```
```shell
###############
function scramble ()
{
typeset -i index quescount
questions=$(\$!)
quescount=\$\{#questions[*]\}      # Number of elements
((index=quescount-1))
while [[ \$index > 0 \% ]]; do
   ((target=RANDOM \% index))
   exchange \$target \$index
   ((index -= 1))
done
}
```
```shell
###############
function ask ()
{
exec 3<\$1
read -u3 ques || exit 2
read -u3 num_opts || exit 2

index=0
choices=()
while (( index < num_opts )); do
    read -u3 next_choice || exit 2
    choices="\${choices[\$]}" "\$next_choice"
    ((index += 1))
done
read -u3 correct_answer || exit 2
exec 3<&-

if [[ \$first_time = true ]]; then
first_time=false
echo -e "You may press the interrupt key at any time to quit.\n"
fi

PS3="\$ques"    "                               # Make \$ques the prompt for select
                                   # and add some spaces for legibility.
select answer in "\${choices[\$]}"; do
   if [[ -z "\$answer" ]]; then
       echo "Not a valid choice. Please choose again.
   elif [[ "\$answer" = "\$correct_answer" ]]; then
       echo "Correct!"
       return 1
   else
       echo "No, the answer is \$correct_answer."
       return 0
   fi
done
}
```
```