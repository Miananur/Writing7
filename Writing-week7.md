# State management
Tidak wajib untuk digunakan, tapi apabila kita memiliki aplikasi yang sudah cukup besar maka kita perlu karena kita akan mempunyai banyak component dan untuk menghubungkan component 1 ke yang lainnya akan lebih mudah jika kita menggunakan state.
State management yang sering dipake : redux dan react context.

## Redux, 
adalah salah satu library yang ukurannya sangat kecil (2 KB). 
Fitur redux : 
* Predictable : Dia punya sebuah siklus yang searah
  ![img 1](photo/2.png)
  ket siklus redux : ketika UI ada sebuah request dia akan langsung ke action, ketika action terjadi dia akan langsung ke reducer, ketika reducer terjadi dia akan lgsg update ke store, dari store akan ngambil lagi datanya dan akan langsung kirim lagi ke UI.
* Centralized
* Debuggable
* Flexible : Bisa memakai UI layer apa saja.
Penjelasan siklus redux 

1. Redux store berfungsi untuk menahan state kita supaya aman. Jika kita pakai redux, redux ini hanya akan punya satu buah store, jadi semua data aplikasi hanya akan disimpan kedalam satu buah tempat penyimpanan state yang sama.
2. Action, sebuah aksi yang hanya read only, hanya bersifat perintah tanpa ada tindakan. Dalam action akan ada yang namanya "Dispatch" yang bertugas untuk mengirimkan sesuatu.
3. Reducer, Sebagai pelaksana. yang ngelakuin semua perintah dari action adalah reducer. Reducer yang akan melakukan perubahan ke store jika perintah sudah di verifikasi.
### Step cara memakai Redux
1. install axios "npm install react-redux axios @reduxjs/toolkit" paa terminal vscode.
2. membuat store dan memasukan ke index.js. masuk ke index.js lalu masukan :
   import {Provider} from 'react-redux
   lalu panggil provider pada return. bungkus tag App dengan tag provider, seperti :
   <Provider>
   <App/>
   </Provider>
3. Buat store menggunakan configure store. Caranya buat satu buah folder terpisah, lalu buat file didalamnya.
   didalam file ketik sebagai berikut :
   import {configureStore} from '@reduxjs/toolkit'

   const store = configureStore({
    reducer:{
        tes:"test"
    }
   })

   export default store
4. Lalu import folder store ke index.js
   import store from "./store
5. baru masukan 'store' kedalam tag provider
   <Provider store={store}>
   <App/>
   </Provider>
6. Buat satu buah folder bernama "Books" di dalam folder src>component, lalu buat file di dalam folder tersebut. file 1 isi dengan kodingan biasa dulu saja, dengan ketik "rafce". lalu file 2 isi sebagai berikut :
   import {createSlice} from '@reduxjs/toolkit'

   const initialState = {
    totalBook:10
   }

   const bookSlice = createSlice({
    name:'book',
    initialState,

    //reducers yang input
    reducers:{
        //borrow termasuk kedalam action
        borrow: (state) => {
            state.totalBook--; //jadi bukunya jika dipinjam maka totalBook akan bekurang
        }
    }
   })

   export default bookSlice.reducer;
7. Pada App.js import file yang telah dibuat tersebut.
8. Lalu masuk ke file dalam folder store lagi dan import bookSlice
   import {configureStore} from '@reduxjs/toolkit'
   import bookReducer from '../Components/Books/BooksSlice'

   const store = configureStore({
    reducer:{
        tes:"test"
        book: bookReducer,
    }
   })
9. Cek data store di inspect>redux>state. install dulu extention 'Redux DevTools' pada chrome buat bisa liat. 
10. Memunculkan state dari store redux. caranya :
    * masuk ke file 1 pada folder Books, lalu import useSelector
        import {useSelector} from 'react-redux'

        const BooksView = () => {

            //nama 'totalBooks' harus sama dengan yang ada pada file 2 folder Books
            //'state.book' booknya itu tergantung name pada file 2 folder Books
            const totalBooks= useSelector((state)=>state.book.totalBooks)
            console.log("tes", total.Books)

            return (
                <div>
                    <h1>File 1</h1>
                    <h1>Total Books: {totalBooks}</h1>
                <div>
            )
        }

        export default BooksView;



