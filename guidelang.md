# The Guidance Language

The guidance language is a fictional programming language. It is used to help students understanding main concepts in programming languages.

The main purpose of this language is to program fellow students in accomplishing simple tasks such as search and recovery of particular objects in a known environment.

A program (or script) written in this language consists of set of instructions, also known as **statements**.

## Statements

### ACTION statements

Action statements represent the simplest actions that can be performed by a person being guided. 

```guidelang
step forward
turn left
turn right
turn back
grab <OBJECT>
```

* When using the grab statement (`grab <OBJECT>`), the `<OBJECT>` should be replaced with the desired item. For example:

    ```guidelang
    grab <pencil>
    ```

### TESTS statements

Test statements represent the questions that a person being guided can ask. Each question can only be answered with one of the `RESULT` options on the right side.

```guidelang
can see <OBJECT>?   | RESULT (true,false)
can reach <OBJECT>? | RESULT (true,false)
where is <OBJECT>?  | RESULT (front, back, left, right, unknown)
```

* The term `<OBJECT>` should be replaced with the desired object. For example:

    ```guidelang
    can see <pencil>?
    ```

<div style="page-break-after: always;"></div>

### SPECIAL statement

The following special statements can be used in a guidance script.

#### Go to

```guidelang
go to line NUMBER
```

* A **go to statement** can refer the person being guided to continue the execution from a particular line in your script. For example, to walk forever, you could do:

    ```guidelang
    1 | step forward
    2 | go to line 1
    ```

#### Conditional

```guidelang
if TEST = RESULT then
    ACTION or SPECIAL statements
```

* A **conditional statement** can be used to ask a question.
* If the result matches the answer of the test, the inner set of statements (i.e., **inner block**) is executed.
* The *inner block should indented*, i.e., spaced right from the conditional statement. For example:

    ```guidelang
    if can reach <pencil> then
        grab <pencil>
        turn back
        step forward
    ```

#### Procedures

```guidelang
procedure PROCEDURE_NAME(PARAMETERS)
    ACTION or SPECIAL statements

execute PROCEDURE_NAME
```

* A **procedure statement** declares a set of statements that can be memorized.
* They are not executed right away.
* The statements of a procedure are executed the **execute statement** is used.
* When declaring a procedure, choose a unique `PROCEDURE_NAME`.
* Procedures can receive one or more parameters, to be used on the statements. For example:

    ```guidelang
    procedure grab_if_can_reach(object)
        if can reach object? = true then
            grab object
    ```

## Examples

In the following, you can see a few examples of scripts using the the guidance language.

### Walk towards a wall

```guidelang
1 | if can reach <wall>? = false then
2 |     step forward
3 |     go to line 1
```

### Turn to wall

```guidelang
1 | if where is <wall>? = right then
2 |     turn right
3 | if where is <wall>? = left then
4 |     turn left
5 | if where is <wall>? = left then
6 |     turn left
```

### Go to wall

```guidelang
 1 | procedure go_to_wall()
 2 |    if where is <wall>? = right then
 3 |        turn right
 4 |    if where is <wall>? = left then
 5 |        turn left
 6 |    if where is <wall>? = left then
 7 |        turn left
 8 |    if can reach <wall>? = false then
 9 |        step forward
10 |        go to line 1
11 |
12 | execute go_to_wall()
```

### Exit a room and get an object

```guidelang
 1 | procedure turn_towards(object)
 2 |    if where is object? = right then
 3 |        turn right
 4 |    if where is object? = left then
 5 |        turn left
 6 |    if where is object? = left then
 7 |        turn left
 8 | 
 9 | procedure walk_towards(object)
10 |    if can reach object? = false then
11 |        step forward
12 |        go to line 10
13 | 
14 | turn_towards(<door>)
15 | walk_towards(<door>)
16 | grab <door handle>
17 | step forward
18 | turn_towards(<pencil>)
19 | walk_towards(<pencil>)
20 | grab <pencil>
```