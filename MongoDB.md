### SO SANH SU KHAC NHAU GIUA MongoDB va SQL DB (Co so du lieu quan he)

    SQL DB      |       MongoDB
    Table       |       Collection
    Row         |       Document
    Column      |       Field
                
              
### XEM CAC DATABASE TRONG SYSTEM

    show dbs

### TAO 1 DATABASE

    use ten_database

### SU DUNG DATABASE

    use ten_db

### XEM DATBASE DANG SU DUNG (current database)

    db

### XOA DATABASE DANG SU DUNG

    db.dropDatabase()


### XEM TAT CA CAC COLLECTION CO TRONG DATABASE

📌 Collection co kieu du lieu la 1 Array.

    show collections

### TAO COLLECTION

    db.createCollection(collectionName, option)

Vi du: db.createCollection("admin",{validator:{$or:[{name: {$type:
 "string" }},{password: {$type: "string"}},{email: { $regex: "/@gmail\.com"}}]}}
)

=> Trong doan tren da rang buoc du lieu cho trường name và password có kiểu dữ liệu là string, email bắt buộc phải có đuôi là @gmail.com

### XOA COLLECTION

    db.collectionName.drop()

### THEM (INSERT) DU LIEU VAO COLLECTION

MongoDB đã cung cấp cho chúng ta 3 phương thức để thực hiện việc thêm mới dữ liệu vào trong collection. Bao gồm các phương thức sau:

+ insert
+ insertOne
+ inserMany

📌 Insert : Phương thức insert trong MongoDB dùng để thêm mới một hoặc nhiều dữ liệu vào trong MongoDB.

    db.conlectionName.insert(data)

=> Trong do, data co the la 1 Object chua cai Field va gia tri tuong ung.

Vi du: db.admin.insert({
  name: "Iron Man",
  password: "admin",
  email: "ironman@example.com"
})

📌 insertOne : Phương thức insertOne trong MongoDB có tác dụng cho phép chúng ta insert một dữ liệu vào trong MongoDB trên một lần khai báo.

    db.collectionName.insertOne(data)

📌 insertMany : Phương thức insertMany cho phép chúng ta thêm mới nhiều dữ liệu vào trong MongoDB.

    db.collectionName.insertMany(data)

### TRUY VAN DU LIEU TRONG MONGODB

###  LAY TAT CA DU LIEU TRONG COLLECTION

    db.collectionName.find()

=> Du lieu tra ve se la 1 Object.

- Nếu như bạn muốn dữ liệu được trả về được hiển thị theo cấu trúc đã được định sẵn thì chỉ cần thêm hàm pretty() vào phía sau hàm find().

    db.collectionName.find().pretty()

### TRUY VAN DU LIEU CO DIEU KIEN TRONG MONGODB

Để truy vấn có điều kiện trong MongoDB thì bạn cũng sử dụng cú pháp tương tự như phần 1, nhưng lúc này chúng ta sẽ chèn thêm điều kiện vào trong hàm find().

    db.collection.find(condition)

=> Trong do, condition la 1 Object chua cac menh de dieu kien

+ TOAN TU TRONG MONGODB

📌 Bằng (Equality) : {key: value}
📌 Nhỏ hơn (Less Than) : {key: {$lt: value}}
📌 Nhỏ hơn bằng (Less Than Equals) : {key: {$lte: value}}
📌 Lơn hơn (Greater Than) : {key: {$gt: value}}
📌 Lớn hơn bằng (Greater Than Equals) : {key: {$gte: value}}
📌 Khác (Not Equals) : 	{key: {$ne: value}}
📌 Trong khoang (In) : {key: {$in: [value1, value2,..]}}
📌 Không Thuộc (Not In) : {key: {$nin: [value1, value2,..]}}

Vi du: 

- Lay ra nhan vien co ten la Iron Man : db.admin.find({name: "Iron Man" }).pretty()
- Lay ra nhan vien co do tuoi < 30 : db.admin.find({age: { $lt: 30}).pretty()

### TRUY VAN NHIEU DIEU KIEN TRONG MONGODB

+ Ket hop them voi cac toan tu AND, OR, ...

📌 AND

- Lấy ra admin có tên Iron Man và có tuổi là 28 trong collection admin :

db.admin.find({
    name: "Iron Man",
    age: 28
})

📌 OR

db.collectionName.find({
    $or : [
        {key1: value1},
        {key2: value2},
        ...,
        {keyn: valuen}
    ]
}).pretty()

Vi du: 
- Lấy ra tất cả các admin có tuổi bằng 28 hoặc name là Iron Man trong collection admin:

db.admin.find({
    $or : [
        {age: 12},
        {name: "Vu Thanh Tai"},
    ]
}).pretty()

📌 Ket hop ca AND va OR

Vi du:

- Lấy ra tất cả các admin có tuổi bằng 28 hoặc password bằng admin và có name là Iron Man trong collection admin.

db.admin.find({
    $or : [
        {age: 28},
        {password: "admin"},
    ],
    name: "Iron Man"
}).pretty()

### GIOI HAN SO LUONG BAN GHI TRONG MONGODB

📌 Giới hạn số lượng bản ghi được lấy ra khi truy vấn thì các bạn chỉ cần thêm phương thức limit() vào phía sau phương thức find()

db.collectionName.find().limit(number)

📌 Trong một số trường hợp, bạn muốn bỏ qua một hoặc nhiều bản ghi đầu trong số bản ghi được lấy ra thì trong MongoDB đã cung cấp cho chúng ta phương thức skip() 

db.collectionName.find().skip(numberSkip)

Vi du: 

- Bỏ qua 3 bản ghi đầu trong số bản ghi được lấy ra : db.admin.find().skip(3)

### SAP XEP DU LIEU TRONG MONGODB

📌 Để có thể sắp xếp dữ liệu được trả về trong MongoDB thì các bạn sử dụng phương thức sort()

db.admin.find().sort({field: orderMode})

=> Trong do:

👉 field : là trường chọn để sắp xếp dữ liệu.
👉 orderMode : là kiểu sắp xếp. Trong đó: 1 - tang dan ; -1 - giam dan

Vi du: 

- Lấy ra tất cả các document có trong collection và sắp xếp theo độ dài của trường name giảm dần : db.admin.find().sort({name: -1})

### UPDATE DU LIEU TRONG MONGODB




HAPPY CODING ️🎉️🎉️🎉
