
Class                WMC     CBO    LCOM    Quick notes


Bank                14      4       0       Everything seems fine


BankAccount         20      4       44      That's a lot of LCOM


Person              23      3       79      That's a lot of LCOM


The Person class has the highest WMC.

Bank and BankAccount have both the highest CBO (4).

The BankAccount class seems to be the most worrying, the Bank method have a low WMC and a low LCOM which is fine, the Person class has bad metrics but is quite simple for now, only getters and setters whereas BankAccount has bad metrics too but is much more complicated with more complex methods overall.