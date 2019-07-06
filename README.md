# Modul-7_Struktur-Data
Hashing

Hashing - Pencarian akan lebih cepat lagi jika semua data pada list terletak tepat berada ditempatnya masing-masing, 
sehingga pencarian dilakukan hanya dengan satu kali proses perbandingan saja.
Istilah dasar pada algoritma Hashing :
•	Hash Table, yaitu sebuah tempat penyimpanan data, yang dibuat sedemikian rupa, sehingga dapat memudahkan pencarian.
•	slot, yaitu posisi (indeks) yang terdapat pada hash table sebagai tempat penyimpanan setiap data. 
  Karena slot berfungsi seperti halnya indeks.
•	Hash function, yaitu suatu fungsi yang memetakan antara data dengan slot di dalam hash table.

-------------------------------------------------------------------------------------------------------------------------------
Fungsi Hash - data didalam list disusun berdasarkan nilai hash, 
dan pencarian data dilakukan berdasarkan nilai hash dari hash function ini.
Contoh hash function adalah remainder function. Parameter berupa nilai data,
dan nilai balik berupa modulus dari data tersebut dengan sebuah angka (misal ukuran dari tabel). 
Fungsi ini hanya menghitung modulus dari suatu data, contoh, data dengan nilai 54, maka nilai hash = 54 % 11, yaitu 4.
 
 .Data  Nilai Hash 
   54	|	10   
   56	|	4  
   93	|	5  
   17	|	6 
   77	|	0 
   31	|	9 

    def remainderFunction (data,num):
        return (data%num)

    def createHashTable(num):
        temp=[]
        for i in range(num):
            temp.append('none')
        return(temp)
    def putData(data,table):
        for i in range(len(data)):
            ind=remainderFunction(data[i],len(table))  
            table[ind]=data[i]
        return(table)

    def searchHash(data,table):
        hashVal=remainderFunction(data,len(table))
        if data==table[hashVal]:
            return True
        else:
            return False

    a=[54, 26, 93, 17, 77, 31]
    hashTable=createHashTable(11)
    print(hashTable)

    hashTable=putData(a,hashTable)
    print(hashTable)

    searchHash(93,hashTable)

Fungsi Hash untuk String - Berikut fungsi untuk mendapat nilai ascii dari suatu string.

def strVal(strData):
    temp=0
    for i in range (len(strData)):
        temp=temp+ord(strData[i])
    return(temp)

strVal('indonesia')

print(strVal('dia'))
print(strVal('adi'))


Collusion
Perfect Hash Function meminimalisir terjadinya colluision, akan tetapi terkadang, collusion ini tidak dapat dihindari, sehingga diperluka penanganan atau yang dikenal dengan collusion resolution.

Open addressing, yaitu pencarian slot kosong yang siap ditempati oleh data baru.

Linear Probing, yaitu mencari slot kosong dengan cara mengunjungi slot-slot ini satu persatu, dimulai dari slot tempat terjadinya collusion.

def linearProbing(ind,hashTable,data):
    count=ind
    found=False
    
    while (count!=ind-1) and not(found):
        
        if hashTable[count]=='none':
            found=True
            hashTable[count]=data
            
        else:
            count=count+1
            if count==len(hashTable)-1:
                count=0
    return(hashTable)

def putData3(a,hashTable,functionName):
    
    for i in range(len(a)):
       
        if functionName=='reminder':
            ind=remainderFunction(a[i],len(hashTable))   
            
        elif functionName=='midSq':
            ind=midSqFunction(a[i],len(hashTable))  
        
       
        if hashTable[ind]=='none':
            hashTable[ind]=a[i]
        else:
            hashTable=linearProbing(ind,hashTable,a[i])    
        
    return(hashTable)

a=[54, 26, 93, 17, 77, 31]
hashTable=createHashTable(11)
print(hashTable)
hashTable=putData3(a,hashTable,'reminder')
print(hashTable)

a=[54, 26, 93, 17, 77, 31,44,55,20]
hashTable=createHashTable(11)
print(hashTable)
hashTable=putData3(a,hashTable,'reminder')
print(hashTable)
