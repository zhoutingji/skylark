API List for virgo
==================

quick overview of api.

Types Defination
-----

```
data            dict of "name:value" pairs
field           instance of Field 
expr            instance of Expr
fldAssign       assignment like "field=value"
fieldname       field.name (str)
primarykey      instance of PrimaryKey
model           model class,inherited from Model
modelObj        instance of model
joinmodel       instance of JoinModel
select_results  instance of SelectResult
cursor          instance of MySQLdb.cursors.Dictcursor
```

API
---

```python

    return                  function type       function

class  Database():

    str                     classattribute      Database.SQL

    int                     classattribute      Database.query_times

    None                    classmethod         Database.config(**configs)

    cursor                  classmethod         Database.execute(str)

class Model(*fldAssign,**data):

    dict                    instanceattribute   modelObj._data

    *                       instanceattribute   modelObj.fieldname                      

    field                   classattribute      Model.fieldname

    str                     classattribute      Model.table_name

    primarykey              classattribute      Model.primarykey

    model                   classmethod         Model.create(*fldAssign,**data)

    int                     classmethod         Model.update(*fldAssign,**data)

    select_results          classmethod         Model.select(*fldAssign)

    int                     classmethod         Model.delete()

    model                   classmethod         Model.where(*expr,**data)

    model                   classmethod         Model.at(int)

    model                   classmethod         Model.orderby(field,desc=bool)

    joinmodel               classmethod         Model.__and__(arg) arg:model or joinmodel  # operator: Model & arg

    bool                    classmethod         Model.__contains__(modelObj)  # operator: modelObj in model

    int                     instancemethod      ModelObj.save()

    int                     instancemethod      ModelObj.destroy()

class JoinModel(*model):

    str                     classattribute      JoinModel.table_name

    list of primarykey      classattribute      JoinModel.primarykey

    joinmodel               classmethod         JoinModel.where(*expr)

    joinmodel               classmethod         JoinModel.orderby(field,desc=bool)

    select_result           classmethod         JoinModel.select(*field)

    int                     classmethod         JoinModel.update(*field)

    joinmodel               classmethod         JoinModel.__and__(arg) arg:model or joinmodel  # operator: JoinModel & arg

class SelectResult(model):

    int                     instanceattribute   select_result.count

    model/tuple of models   instancemethod      select_result.fetchone()

    iterator                instancemethod      select_result.fetchall()

class Field():

    str                     instanceattribute   field.name

    str                     instanceattribute   field.fullname

    bool                    instanceattribute   field.primarykey

    model                   instanceattribute   field.model

    expr                    instancemethod      field.__lt__(arg) arg:field or value  # operator:field < arg

    expr                    instancemethod      field.__le__(arg) arg:field or value  # operator:field <= arg

    expr                    instancemethod      field.__gt__(arg) arg:field or value  # operator:field > arg

    expr                    instancemethod      field.__ge__(arg) arg:field or value  # operator:field >= arg

    expr                    instancemethod      field.__ne__(arg) arg:field or value  # operator:field != arg

    expr                    instancemethod      field.__eq__(arg) arg:field or value  # operator:field == arg

    expr                    instancemethod      field.__add__(arg) arg:field or value  # operator:field + arg

class Expr(left,right):

    str                     instanceattribute   expr.op

    str                     instanceattribute   expr._tostr

    expr                    instancemethod      expr.__and__(arg) arg:expr  # operator:expr & expr

    expr                    instancemethod      expr.__or__(arg) arg:expr  # operator:expr | expr

```