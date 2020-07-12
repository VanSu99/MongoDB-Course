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
<<<<<<< HEAD
=======

>>>>>>> 62a6febe01fea945ebe048872f5442d4ce29102b

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

### ️TRUY VAN DU LIEU TRONG MONGODB

### ️🎯 LAY TAT CA DU LIEU TRONG COLLECTION

    db.collectionName.find()

=> Du lieu tra ve se la 1 Object.

- Nếu như bạn muốn dữ liệu được trả về được hiển thị theo cấu trúc đã được định sẵn thì chỉ cần thêm hàm pretty() vào phía sau hàm find().

    db.collectionName.find().pretty()

### ️🎯 TRUY VAN DU LIEU CO DIEU KIEN TRONG MONGODB

Để truy vấn có điều kiện trong MongoDB thì bạn cũng sử dụng cú pháp tương tự như phần 1, nhưng lúc này chúng ta sẽ chèn thêm điều kiện vào trong hàm find().

    db.collection.find(condition)

=> Trong do, condition la 1 Object chua cac menh de dieu kien

️🎯 TOAN TU TRONG MONGODB

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

### ️🎯 TRUY VAN NHIEU DIEU KIEN TRONG MONGODB

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

### ️🎯BONUS THEM CACH TRUY VAN xyz

- Lay cac title trong collection posts

    db.posts.find().forEach(function(doc){
        print('Blog title: ' + doc.title)
    })

### ️🎯 GIOI HAN SO LUONG BAN GHI TRONG MONGODB

📌 Giới hạn số lượng bản ghi được lấy ra khi truy vấn thì các bạn chỉ cần thêm phương thức limit() vào phía sau phương thức find()

    db.collectionName.find().limit(number)

📌 Trong một số trường hợp, bạn muốn bỏ qua một hoặc nhiều bản ghi đầu trong số bản ghi được lấy ra thì trong MongoDB đã cung cấp cho chúng ta phương thức skip() 

    db.collectionName.find().skip(numberSkip)

Vi du: 

- Bỏ qua 3 bản ghi đầu trong số bản ghi được lấy ra : db.admin.find().skip(3)

### ️SAP XEP DU LIEU TRONG MONGODB

📌 Để có thể sắp xếp dữ liệu được trả về trong MongoDB thì các bạn sử dụng phương thức sort()

    db.admin.find().sort({field: orderMode})

=> Trong do:

👉 field : là trường chọn để sắp xếp dữ liệu.

👉 orderMode : là kiểu sắp xếp. Trong đó: 1 - tang dan ; -1 - giam dan

Vi du: 

- Lấy ra tất cả các document có trong collection và sắp xếp theo độ dài của trường name giảm dần : db.admin.find().sort({name: -1})

### UPDATE DU LIEU TRONG MONGODB

### 🎯 SUA DOI MOT BAN GHI TRONG MONGODB

+ Để sửa đổi một bản ghi duy nhất trong MongoDB thì các bạn sử dụng phương thức updateOne()

    db.collectionName.updateOne(
        filter,
        update,
        {
            upsert: <boolean>,
            writeConcern: <document>
            collation: <document>,
        }
    )

Trong do:
    + filter là một object chứa các tiêu chí lựa chọn bản ghi update (sử dụng cú pháp selector).
    + update là object chứa dữ liệu sửa đổi trên bản ghi.
    + upsert là một boolean cấu hình điều gì sẽ xảy ra khi không có bản khi khớp với filter. Nếu upsert = true thì nó sẽ thêm mới bản ghi đó nếu không có bản ghi nào khớp với filter và sẽ không có điều gì xảy ra nếu upsert = false. Mặc định thì upsert = false.
    + writeConcern là một document chứa write concern.
    + collation là một document chứa các quy tắc.

Vi du:
-  Sửa name của admin có tuổi = 28 thành Thor.

    db.admin.updateOne(
        {age: 28},
        {
            $set: {
                name: "Thor"
            }
        }
    )

### 🎯 SUA DOI NHIEU BAN GHI TRONG MONGODB

Vi du:
- Sửa name của admin có name = "Iron Man" thành 'Hulk'.

    db.admin.updateMany(
        {name: "Iron Man"},
        {
            $set: {
                name: "Hulk"
            }
        }
    )

### 🎯 SUA DOI BAN GHI TRONG MONGODB

Vi du: 
- Sửa đổi name của một bản ghi duy nhất có name là "Hulk" thành "SuperSoi".

db.admin.updateOne(
    {name: "SuperSoi"},
    {
        $set: {
            name: "Hulk"
        }
    },
    {
        multi : false
    }
)

+ multi là một boolean cấu hình xem có cho phép sửa đổi nhiều bản ghi hay không, multi bằng true là cho phép và ngược lại bằng false thì là không. Mặc định thì thuộc tính này có giá trị là false.

### XOA DU LIEU MONGODB

- Để có thể xóa dữ liệu trong MongoDB thì các banj sử dụng phương thức remove() 

    db.collectionName.remove(
    query,
    {
        justOne: <boolean>,
        writeConcern: <document>,
        collation: <document>
    }
    )

Trong do:
    + query là object (hay còn gọi là document) chứa các câu truy vấn để lọc dữ liệu.
    + justOne là tham số cấu hình số lượng bản ghi có thể xóa khi query thực thi khớp.
        - Nếu justOne: true thì nó sẽ chỉ xóa 1 bản ghi duy nhất.
        - Nếu justOne: false thì nó sẽ xóa tất cả các bản ghi khớp với điều kiện query.

Vi du:
- Xóa một admin có name = "Toidicode" và có age = 18.

    db.admin.remove(
    {
        name: "Toidicode",
        age: 18
    }
    )
    


HAPPY CODING ️🎉️🎉️🎉
