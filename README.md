# TerminalPyth

Library that allows you to call terminal commands in python whithout discarding director changes (unlike os.system() command does).

`Install:`

    $ pip install terminalpyth

`Usage:`

    import terminalpy

Create a terminalpy object. Pass True or False as argument if you want (or not) to have back the output.

    trm = terminalpy.Terminal(output=True)

Only one straight-forward method: type. Pass inside it the command you want to be executed.

    output = trm.type('pwd')

    # in this case, returns path to the current directory, which in this case is stored in "output"

It works with pretty much every terminal command. 

To use "sudo", if you are not in a terminal session itself, you must add the "-S" option, to read the password from your IDE (e.g. Pycharm).

    trm.clear()

This command clears the memory of the directory changes, returning back to the project foler.

    trm.setOutput(output=False)

Changes the state of the return action. If "False", there will be no return value, otherwise there will. \
The method allows to change the state during the session

`Examples`:

Imagine a basic directory tree:

- home
    - python
        - project1
            - main.py
        - project2
            - prj2.py
    - c++
        - project3
 
The code:

    # /home/python/project1/main.py             |       # /home/python/project1/main.py
    import terminalpy                           |       import os
                                                |
    trm = terminalpy.Terminal(True)             |       os.system('pwd')
                                                |       # output: /home/python/project1/
    print(trm.type('pwd'))                      |
    # output: /home/python/project1             |       os.system('cd ..')
                                                |       os.systenm('ls')
    trm.type('cd ..')                           |       # output: main.py
    trm.type('ls')                              |
    # output:   project1                        |       os.system('cd ..')
    #           project2                        |       os.system('cd c++') # Error: Directory not found
                                                |       os.system('cd project3') #Error: Directory not found
    trm.type('cd ..')                           |       os.system('pwd')
    trm.type('cd c++')                          |       # output: /home/python/project1
    trm.type('cd project3')                     |
    print(trm.type('pwd'))                      |
    # output: /home/c++/project3                |
                                                |
    trm.clear()                                 |
    print(trm.type('pwd'))                      |
    # output: /home/python/project1             |
    
This is an example of the difference between TerminalPyth and the standard os.system(). TerminalPyth works with every terminal command, just like a normal terminal call, but allows to keep directory change.
  
