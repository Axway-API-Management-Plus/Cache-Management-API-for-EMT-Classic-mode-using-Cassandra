## The Scripts are based on the Jython which we used to perform CRUD function in the KPS that can be used a distributed Cache in EMT and Classic solution.

Here are the details of the 5 API's :-

### 1. Create new Record - This policy will create a new entry in the Cassandra cache table with a value of TTL (Time to live - till the time new entry will stay in the Cassandra cache table).

 

URL - http://<IP>:<port>/create?data=test&TTL=30

 

Jython Create Script

========================================================================================

from java.util import HashMap
from com.vordel.kps import Table, ObjectExists

def invoke(msg):
data = msg.get("data")
TTL = int (msg.get("TTL"))
recordhash = HashMap()
# If the primary key is auto-gererated then, the next line should be deleted
recordhash.put("id", data)
# Repeat next line for each of the non-auto-generated properties properties, note that if TTL is non-zero then, all non-auto-generated properties must be set
recordhash.put("data", data)

try:
recordhash = Table.createRecord("cache", recordhash, TTL)

except ObjectExists:

return False
return True

========================================================================================

 

### 2. Delete a record -  This policy is to delete a Cassandra entry.

 

URL - http://<IP>:<port>/delete?data=test

 

Jython Delete Script

========================================================================================

from com.vordel.kps import Table, ObjectNotFound

def invoke(msg):
data = msg.get("data")
try:
record = Table.deleteRecord("cache", data)

except ObjectNotFound:

return False
return True

========================================================================================

 

### 3. Extend TTL for a record - This policy is to update the TTL value of a entry that already exist in the Cassandra cache table.

 

URL - http://<IP>:<port>/TTL?data=test&TTL=30

 

Jython Script

========================================================================================

from java.util import HashMap
from com.vordel.kps import Table, ObjectNotFound

def invoke(msg):
data = msg.get("data")
TTL = int (msg.get("TTL"))
record = HashMap()
record.put("id", data)

record.put("data", data)

try:
record = Table.readRecord("cache", data)
Table.updateRecord("cache", record, TTL)


except ObjectNotFound:
return False
return True

========================================================================================

 

 

### 4. Read a record - This policy is to check if any entry exist in the Cassandra cache table.

 

URL - http://<IP>:<port>/read?data=test

 

Jython Read Script

========================================================================================

from com.vordel.kps import Table, ObjectNotFound

def invoke(msg):
data = msg.get("data")
try:
record = Table.readRecord("cache", data)

except ObjectNotFound:

return False
return True

========================================================================================

 

5. Update a record - This policy is to update any one existing entry in the Cassandra cache table and then update it with the new record and TTL value's.

 

URL - http://<IP>:<port>/update?data=test&TTL=30&id=test

 

Jython Update Script

========================================================================================

from java.util import HashMap
from com.vordel.kps import Table, ObjectNotFound

def invoke(msg):
data = msg.get("data")
id = msg.get("id")
TTL = int(msg.get("TTL"))
updated = msg.get("update")
record = HashMap()
record.put("id", id)

record.put("data", data)

try:
record = Table.readRecord("cache", id)


record = Table.updateRecord("cache", record, TTL)


except ObjectNotFound:

return False
return True

========================================================================================

 