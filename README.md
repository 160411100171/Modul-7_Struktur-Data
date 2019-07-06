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
 
 .Data | Nilai Hash 
 
   54	 |	10   
 
   56	 |	4  
   
   93	 |	5  
   
   17	 |	6 
   
   77	 |	0 
   
   31	 |	9 

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

--------------------------------------------------------------------------------------------------------------------------------
Fungsi Hash untuk String - Berikut fungsi untuk mendapat nilai ascii dari suatu string.

    def strVal(strData):
        temp=0
        for i in range (len(strData)):
            temp=temp+ord(strData[i])
        return(temp)

    strVal('indonesia')

    print(strVal('dia'))
    print(strVal('adi'))

-----------------------------------------------------------------------------------
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


---------------------------------------------
Tugas Praktikum
Buatlah fungsi-fungsi yang diperlukan dalam pencarian berdasarkan menggunakan konsep hashing, dan penanganan collusion dengan chaining. Fungsi-fungsi tersebut antara lain : 

1.	Hash Function yaitu fungsi hash yang menggunakan remainder function, dengan dua argument atau parameter, yaitu :

    a.	data yang akan dimasukkan ke dalam table hash 

    b.	bilangan modulo 

Sedangkan return value nya berupa adalah slot atau posisi data pada hash table.
 
Contoh berikut adalah eksekusi reminderfunction dengan argument data berupa 55, dan bilangan modulo adalah 10, sehingga output yang dihasilkan adalah 55 % 10 = 5.

    Slot=remainderFunction(55,10)
    Print(slot)
    --------------------------------------
    5

2.	create Hash Table, yaitu fungsi pembuatan hash table. Gunakan list 2D pada pembuatan hash table ini, karena dibutuhkan untuk penanganan collusion dengan chaining. Argumen yang terdapat pada fungsi ini adalah ukuran dari hash table, sedangkan return value berupa Hash table yang telah terbentuk (berupa list 2D, dengan nilai default adalah [None] 

Berikut adalah inisialisasi hash table dengan ukuran 11 :

    hashTable=createHashTable(11)
    print(hashTable)
    --------------------------------------------
    [[None], [None], [None], [None], [None], [None], [None], [None], [None], [None], [None], [None]]

3.	chaining, yaitu fungsi penempatan sejumlah data pada hash table yang telah dibuat. Fungsi chaining ini memiliki argument berupa list data (kumpulan data) yang akan ditempatkan pada hash table, dan hash table yang telah dibuat sebelumnya. Penempatan data yang dibuat berdasarkan metode chaining untuk penanganan collusion. Jika suatu data memiliki nilai hash yang sama (berdasarkan fungsi hash, gunakan remainder function yang telah dibuat), maka data ditempatkan pada slot yang sama, akan tetapi pada indeks yang berbeda 

4.	searchHash, yaitu fungsi pencarian berdasarkan fungsi hash yang telah dibuat sebelumnya. Argumen adalah data yang akan dicari dan hash table yang telah dibuat sebelumnya. Return value adalah False (jika data tidak ada), atau Nomor slot dan indeks jika data ada,

-----------------------------------------------------------------------------------
Jawaban

    def remainderFunction (data,num):
        return (data%num)

    def createHashTable(num):
        temp=[]
        for i in range(num):
            temp.append('none')
        return(temp)
    def chaining(data,table):
        for i in range(len(data)):
            ind=remainderFunction(data[i],len(table))  
            table[ind]=data[i]
            table[ind].append(data[i])
        return(table)

    def searchHash(data,table):
        hashVal=remainderFunction(data,len(table))
        if data==table[hashVal]:
            return True
        else:
            return False

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

    def chaining2(a,hashTable,functionName):

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

    print("====== Nomor 1 ======")
    slot = remainderFunction(55,10)
    print( slot)
    print("====== Nomor 2 ======")
    hashTable = createHashTable(11)
    print(hashTable)
    print("====== Nomor 3 ======")
    a=[54,26,93,17,77,31,44,55,20]
    c = chaining(a,hashTable)
    print(c)
    print("======================")
    ##a=[54,26,93,17,77,31,44,55,20]
    ##hashTable = chaining(a,hashTable)
    ##print(hashTable)
    print("Nomor. 4")
    searchHash(66, hashTable)
    searchHash(54, hashTable)
    searchHash(20, hashTable)
    searchHash(55, hashTable)
    searchHash(100, hashTable)
    print(searchHash)
