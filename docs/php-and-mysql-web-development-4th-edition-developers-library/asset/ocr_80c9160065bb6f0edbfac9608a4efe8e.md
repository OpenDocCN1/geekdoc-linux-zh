# 9.2 Putting PHP to Work

Score Browser," because that script pertains to the grade-keeping project. The other link is to the score_entry.php script that we're about to write:

```
#php
# Grade-Keeping Project home page

require_once 'sampdb_pdo.php';

$title = 'Grade-Keeping Project';
html_begin ($title, $title);
?>

</p>
<a href='/cgi-bin/score_browse.pl'>View</a> test and quiz scores
</p>
</p>
<a href='score_entry.php'>Enter or edit</a> test and quiz scores
</p>

</p>
?>
html_end ();
?>
```

You can find this index.php script in the phpapi/gp directory of the sampdb distribution. Copy it to the gp directory of your Web server document tree.

Let's consider how to design and implement the score_entry.php script that will let us enter a set of test or quiz scores or edit existing sets of scores. Entry capability will be useful whenever we have a new set of scores to add to the database. Editing capability is necessary for changing scores later; for example, to handle scores of students who take a test or quiz later than the rest of the class due to absence for illness or other reason (or, perhaps the thought, to correct errors should we happen to enter a score incorrectly). Conceptually, the score entry script operates like this:

+   - The initial page presents a list of known grade events and enables you to choose one, or to indicate that you want to create a new event.

+   - If you choose to create a new event, the script presents a page that enables you to specify the date and event category (test or quiz). After it adds the event to the database, the script redplays the event list page, which at that point will include the new event.

+   - If you choose an existing event from the list, the script presents a score-entry page showing the event ID, date, and category, a table that lists each student in the class, and a Submit button. Each row in the table shows one student's name and current score for the event. For new events, all scores will be blank. For existing events, the scores will be those you entered at some earlier time. You can fill in or change the scores, and then select the Submit button. At that point, the script will enter the scores into the score table or revise existing scores. This operation needs to be done