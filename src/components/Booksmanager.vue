<script setup>
import { createBook, getBooks, deleteBook } from "../api/books";
</script>

<script>
export default {
  name: "Booksmanager",
  data() {
    return {
      books: [],
      newBook: {
        title: "",
        author: "",
        year: 2000,
      },
    };
  },
  methods: {
    async loadbooks() {
      this.books = await getBooks();
    },
    async addBook(book) {
      await createBook(book);
      this.loadbooks();
    },
    async sumbitCreateBook() {
      await this.addBook(this.newBook);
    },
    async removeBook(id) {
      await deleteBook(id);
      await this.loadbooks();
    },
  },
  mounted() {
    this.loadbooks();
  },
};
</script>

<template>
  <main class="flex justify-center items-center flex-col">
    <h1 class="">Könyvtár kezelő felület</h1>
    <form
      @submit.prevent="sumbitCreateBook"
      action=""
      class="w-full my-10 border-2 border-stone-200 p-3 flex flex-col rounded-1"
    >
      <div class="flex flex-col">
        <label for="title" class="">Könyv cím:</label>
        <input
          type="text"
          name="title"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
          v-model="newBook.title"
        />
      </div>
      <div class="flex flex-col">
        <label for="author">konyv szerzoje</label>
        <input
          type="text"
          name="author"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
          v-model="newBook.author"
        />
      </div>
      <div class="flex flex-col">
        <label for="year" class="">kony megjelenesi eve</label>
        <input
          type="number"
          name="year"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
          v-model="newBook.year"
        />
      </div>
      <button
        type="submit"
        class="border-2 bg-blue-200 rounded-lg py-1 p-2 mt-4"
      >
        kaksi
      </button>
    </form>

    <table class="">
      <thead class="">
        <tr class="">
          <th class="">Azonosito</th>
          <th class="">Cim</th>
          <th class="">Szerzo</th>
          <th class="">Megjelenes ev</th>
          <th class="">Muveletek</th>
        </tr>
      </thead>
      <tbody class="">
        <tr v-for="book in books" :key="book.id" class="">
          <td class="">{{ book.id }}</td>
          <td class="">{{ book.title }}</td>
          <td class="">{{ book.author }}</td>
          <td class="">{{ book.year }}</td>
          <td class="">
            <button
            class="border-2 border-rose-500 text-rose-500 rounded-lg px-3 py-1 mt-4 cursor-pointer"
            type="button"
            @click="removeBook(book.id)"
          >
            torles
          </button>
          </td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
