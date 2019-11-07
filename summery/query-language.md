# Summery Task Tracker QL

**Notice**: this is an early draft of the query language reference. This may change in an unexpected way.

## Query Language Definition

The Query Language may have some of the following names:

1) TTQL (Task Tracker Query Language)
2) _tbd_

### Another Query language? Why?

Yes, we need some kind of language to manage tasks in developer-way. It must not implement structures like standart SQL language, and include some instructions for syntactic sugar. Let me explain.

### Create something

Imagine simple task database. And you need to create new task in it. Which SQL you will write?

```sql
INSERT INTO `tasks`(`title`, `assignee`, `due_date`) 
            VALUES('Create this table', 872, DATE_ADD(NOW(), INTERVAL 10 DAY));
```

Feels long, of course. This can be automated by UI and backend operations, but, in QL way you need to do some of this:

```
>>>> #task=> ('Create this table', @username, $today+10d);
>>>> !create #task;
<<>> system: created new task with ID=56432 and assigned it to @username
```

In short, one-line syntax:

```
>>>> !create ('Create this table', @username, $today+10d);
<<>> system: created new task with ID=56432 and assigned it to @username
```

### Update something

If you need to update task info - just replace `!create` with `!update` and write id like this:

```
>>>> #task=> ('Create this table', @username, $today+10d);
>>>> !create #task;
<<>> system: created new task with ID=56432 and assigned it to @username
>>>> !update ('New title') ?? pk=56432
<<>> system: updated `title` in task 56432
```

### Delete something

Remove your tasks using `!delete` like this:

```
>>>> !delete 56432
<<>> system: successfuly deleted task 56432!
```
