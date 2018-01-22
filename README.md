# Assignment One
# Quetion - Take a file count occuerance of each word from the file
I am taking three days for this assginment. I am share my expereance which is giving from code.
# Logic
'''python
import sqlite3,time

start=time.time()

conn = sqlite3.connect('fr.db')
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
      #list2 += [(k)]
   list_data = list(dic.items())
   c.executemany('update info set value = value + ? where name = ?',list1)
   if c.rowcount == 0:
      c.executemany('insert into info values(?, ?)',(list_data))
      conn.commit()
       
def drop_db(info):
    c.execute('drop table info')
    print('Table Droped')
       
dic = {}

fread = open('fr.txt', 'r')

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
'''
