<template>
  <div id="app" class="container">
    <!-- Interpolation -->
    <div class="row my-5">

      <input @keypress.enter.prevent="saveInput" ref="myInput" v-model="msg1">

      <span>{{ msg1 }}</span>

      <comp1 ref="comp1" :msgComp="msg1" @saveChildComponent="saveInput2" />
      <hr>
      <comp1 ref="comp2" :msgComp="msg1" @saveChildComponent="saveInput2" />


      <p v-text="msg2"></p>

      <div v-html="msg3"></div>

      <hr class="mt-3 mb-5" />

      <div v-if="showMsg4" class="alert alert-primary" role="alert">
        {{ msg4 }}
      </div>

      <div
        v-else
        class="alert alert-success d-flex align-items-center"
        role="alert"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          fill="currentColor"
          class="bi bi-exclamation-triangle-fill flex-shrink-0 me-2"
          viewBox="0 0 16 16"
          role="img"
          aria-label="Warning:"
        >
          <path
            d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"
          />
        </svg>
        <div>
          {{ msg5 }}
        </div>
      </div>


      <div
        v-show="showMsg6"
        class="alert alert-danger alert-dismissible fade show"
        role="alert"
      >
        <strong class="mx-5">{{ msg6 }}</strong>
        <button
          type="button"
          class="btn-close closeIcon"
          data-bs-dismiss="alert"
          aria-label="Close"
        ></button>
      </div>

      <br />
      <span v-bind:title="msg7">
        اجعل المؤشر على هذه الجملة
        <span class="redClr" :title="msg8">ما لوني؟</span>
      </span>

      <h4 class="mt-5">Loops</h4>
      <ul class="myList">
        <li v-for="(d, dIndex) in arr" :key="dIndex">
          {{ dIndex + 1 }} - {{ d.name }}
        </li>
      </ul>

       <!-- <button
        v-on:click="addNewToList"
        class="btn btn-success"
        style="width: 140px"
      >
        + أضف جديد
      </button> -->


      <button
        @click="addNewToList"
        class="btn btn-success"
        style="width: 140px"
      >
        + أضف جديد
      </button>

      <div
        v-if="isLoaded"
        class="spinner-border text-warning mx-3"
        role="status"
      ></div>
    </div>
  </div>
</template>

<script>
import comp1 from '@/components/comp1.vue';
export default {
  name: "App",
  components: {
    comp1
  },
  data() {
    return {
      // msg1: "هيا بنا نتعلم الفيو",
      msg1: localStorage.getItem('msg1') || "هيا بنا نتعلم الفيو",
      msg2: "مرحبا بكم في وزارة المالية",
      msg3: '<h1 style="color:blue;text-align:center;">جميل، نحن الآن نتقدم في التعلم</h1>',
      showMsg4: false,
      msg4: "شرط ال if تحقق",
      msg5: "شرط ال else تحقق",
      showMsg6: true,
      msg6: "show تحقق",
      msg7: "أهلا بكم",
      msg8: "لوني أحمر",
      isLoaded: false,
      arr: [
        {
          id: 1,
          name: "محمد",
        },
        {
          id: 2,
          name: "أحمد",
        },
        {
          id: 3,
          name: "خالد",
        },
        {
          id: 4,
          name: "رامي",
        },
      ],
    };
  },
  methods: {
    addNewToList() {
      this.isLoaded = true;
      let chkExisit = this.arr.find((x) => x.name == "سليمان");
      // if (chkExisit) {
      //   this.arr.push({
      //     id: 5,
      //     name: "سليمان",
      //   });
      // }

      setTimeout(() => {
        this.isLoaded = false;
        if (chkExisit) return alert("موجود مسبقا");
        this.arr.push({
          id: 5,
          name: "سليمان",
        });
      }, 1000); // 1second
    },
    saveInput() {
      localStorage.setItem('msg1', this.msg1);
      alert('saved done');
       this.loadData();
    },
    saveInput2(val) {
      this.$refs.comp1.internalMsgComp= val;
      this.$refs.comp2.internalMsgComp= val;
      localStorage.setItem('msg1', val);
      alert('saved done');
      this.loadData();
    },
    loadData() {
      this.msg1= localStorage.getItem('msg1')|| "هيا بنا نتعلم";
    }
  },
  mounted() {
    this.loadData();
    this.$refs.myInput.focus();
  }
};
</script>

<style scoped>
#app .closeIcon {
  font-size: 12px;
  margin: 0 10px;
}
.redClr {
  color: red;
}
.myList {
  list-style: none;
}
</style>