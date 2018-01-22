# Assignment One
# Question - Take a file and count occuerance of each word from the file
for example Input is: "India is my country" and the required Output is 'India':1,'is':1,'my':1,'country':1

# Approach
First i thought we need dictionary,file then i thought need loop and use .split() function and count the word also update into dictionary but when i update into dectionary i got some error. This error came beacuse for loop not iterate then we take list and increse the list then problem was solve then i use nornal syntax for update and insert query(c.execute()) but it too slow then take a help of our boss and use prepraed statement(c.executemany). for using preapraed statement program is too fast.

# Logic:
1. Read whole file through chunk by chunk.
2. create dictionary and insert from chunk
3. Create the table and insert into table from dictionary
4. Update the table through dictionary
5. clear dictionary after update

# Program

```python
import sqlite3,time

start=time.time()

conn = sqlite3.connect('test.db')
c = conn.cursor()

def create_chunk(fread,size=45000000):
   while True:
       data=fread.read(size)
       if not data:
           break
       else:
           yield data

def create_db():
    c.execute('create table if not exists info(name TEXT, value Int)')
    print('table craeated...')

def update(info):
   list1 = []
   for k,v in dic.items():
      list1 += [(v,k)]
   list_data = list(dic.items())
   c.executemany('update info set value = value + ? where name = ?',list1)
   if c.rowcount == 0:
      c.executemany('insert into info values(?, ?)',(list_data))
      conn.commit()
      del list1[:]
       
def drop_db(info):
    c.execute('drop table info')
    print('Table Droped')
       
dic = {}

fread = open('fread.txt', 'r')

for i in create_chunk(fread):
   data = i.split(' ')
   for j in data:
         no = dic.get(j,0)
         dic[j] = no + 1
   dic.clear()
         
         
create_db()
update('info')
#If we want to drop table we comment the drop_db() function
drop_db('info')
fread.close()
c.close()
conn.close()

print("***** Execution time : {} sec ******".format(time.time()-start))
```
