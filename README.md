[Assignment](https://aakashadawle1.github.io/All-Assignment
) / [kettle](https://aakashadawle1.github.io/All-Assignment
/kettle) / [data_structure](https://aakashadawle1.github.io/All-Assignment/data_structure)
# Assignment One
# Question - Take a file and count occurrences of each word from the file
for example Input is: *"India is my country and I love India" and the required Output is 'India':2,'is':1,'my':1,country':1,'and':1,'I':1,'love':1,


# Approach
First, I decided to write approach for the program given. I decided to print the output on the screen but if you print output very large file system may hang so I decided to write into the text file but it was difficult so I rejected it. then I decided to use csv file but updating into csv file was difficult and complicated so the next solution was to use the database as the output storage unit also updating and searching in the database was easy enough.

I use a dictionary as a temporary storage for the occurrences of the word and then updated the database with the dictionary values for the chunk and making dictionary empty after each chunk to stop it from growing very large and thus preventing memory error of dictionary data type in python.

I have to use the sqlite3 module in python for all the database operations.

# Logic:
1. Read the whole file through chunk by chunk.
2. create dictionary and insert from chunk
3. Create the table and insert into table from dictionary
4. Update the table through dictionary
5. clear dictionary after update
6. Repeat 4 and 5

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

