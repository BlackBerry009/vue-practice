<template>
  <div>
    <div class="store">
      <input type="checkbox" class="select-all" v-model="selectAll"/>
      <span class="store-name">DUYI</span>
    </div>
    <ul class="course-list">
      <li class="course" v-for="(course,index) in courseList" :key="course.id">
        <input type="checkbox" 
              class="course-radio" 
              v-model="course.checked"/>
        <div class="poster">
          <img :src="course.poster" alt="">
        </div>
        <div class="content">
          <div class="title">{{ course.title }}</div>
          <div class="price-container">
            <div class="price">${{ course.price }}</div>
            <div class="control-cart">
              <button class="minus-cart" @click="changeNum('-',index)">-</button>
              <input type="text" class="cart-num" v-model.number="course.cart"/>
              <button class="add-cart" @click="changeNum('+',index)">+</button>
            </div>
          </div>
        </div>
      </li>
    </ul>
    <div class="control">
      <div class="select">
        <input type="checkbox" class="select-all" v-model="selectAll"/>
        <span>全选</span>
      </div>
      <div class="price-container">
        <span>合计:</span>
        <span class="price">{{ selectTotalPrice }}</span>
        <button class="accounts">结算({{ selectNum }})</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  created(){
    this.courseList.forEach(course => {
      this.$set(course,'checked',false)
    });
  },
  data() {
    return {
      courseList: [
        {
          poster:
            "https://img.alicdn.com/bao/uploaded/i1/TB1VtAgdlWD3KVjSZFs3KIqkpXa_040950.jpg_80x80.jpg",
          title: "渡一教育 CSS3 深度剖析",
          price: 1299,
          cart: 1,
          id: 0
        },
        {
          poster:
            "https://img.alicdn.com/bao/uploaded/i7/TB1_VJecBWD3KVjSZKPagip7FXa_045814.jpg_80x80.jpg",
          title: "渡一教育 移动端开发课程",
          price: 1148,
          cart: 1,
          id: 1595402664708
        },
        {
          poster:
            "https://img.alicdn.com/bao/uploaded/i2/TB1J.Q4cQxz61VjSZFto7uDSVXa_010347.jpg_80x80.jpg",
          title: "渡一教育 2019年 HTMLCSS零基础入学宝典",
          price: 1,
          cart: 1,
          id: 1596305473062
        },
        {
          poster:
            "https://img.alicdn.com/bao/uploaded/i2/TB1bHwlaCWD3KVjSZSgVbgCxVXa_032434.jpg_80x80.jpg",
          title: "渡一教育 Web前端开发JavaScriptJs课",
          price: 1,
          cart: 1,
          id: 1595413512182
        },
        {
          poster:
            "https://img.alicdn.com/bao/uploaded/i2/TB1MJd3g4z1gK0jSZSgnHevwpXa_014447.jpg_80x80.jpg",
          title: "Web前端开发高级工程师全阶班【渡一教育】",
          price: 12798,
          cart: 1,
          id: 1596302161181
        },
        {
          poster:
            "https://img.alicdn.com/bao/uploaded/i6/TB1xPeAbwaH3KVjSZFpjaLhKpXa_105848.jpg_80x80.jpg",
          title: "渡一教育 Java零基础入门到精通（集合，泛型等）",
          price: 1,
          cart: 1,
          id: 1596300025301
        }
      ]
    };
  },
  computed: {
    selectList(){
      return this.courseList.filter(course => course.checked)
    },
    selectTotalPrice(){
      let totalPrice = 0;
      this.selectList.forEach( course => {
        totalPrice += course.cart * course.price;
      })
      return totalPrice;
    },
    selectNum(){
      return this.selectList.length;
    },
    selectAll: {
      get(){
        return this.courseList.every(course => course.checked)
      },
      set(val){
        this.courseList.forEach( course => {
          course.checked = val;
        })
      }
    },

  },
  methods: {
    changeNum(type,index){
      if(type === '-'){
        if(this.courseList[index].cart === 1) return;
        this.courseList[index].cart--;
      } else if(type === '+'){
        this.courseList[index].cart++;
      }
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

ul,
li {
  list-style: none;
}

body {
  background-color: #f40;
}

#app {
  box-sizing: border-box;
  width: 500px;
  margin: 2px auto 0;
  padding: 20px;
  background-color: #fff;
  border-radius: 5px;
}

#app .store {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

#app .store .select-all {
  margin-right: 10px;
}

#app .store .store-name {
  font-weight: bold;
  font-size: 14px;
}

#app .course-list .course {
  display: flex;
  margin-bottom: 20px;
}

#app .course-list .course-radio {
  width: 16px;
  height: 16px;
  margin-right: 10px;
  transform: translateY(32px);
}

#app .course-list .poster {
  width: 80px;
  height: 80px;
}

#app .course-list .content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 410px;
  margin-left: 10px;
  font-size: 12px;
}

#app .course-list .title {
  margin-top: 10px;
  color: #3c3c3c;
}

#app .course-list .price-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

#app .course-list .price {
  color: #f40;
  font-weight: 700;
}

#app .course-list .control-cart {
  font-size: 0;
}

#app .course-list .cart-num {
  font-size: 10px;
  text-align: center;
  width: 40px;
  padding: 2px 0 3px;
  vertical-align: top;
  border: 1px solid #eee;
  outline: none;
}

#app .course-list .add-cart,
#app .course-list .minus-cart {
  padding: 2px 5px;
  background-color: #fff;
  border: 1px solid #eee;
  outline: none;
}

#app .control {
  display: flex;
  justify-content: space-between;
  font-size: 10px;
}

#app .select {
  display: flex;
  align-items: center;
  color: #3c3c3c;
}

#app .select-all {
  margin-right: 5px;
}

#app .price-container {
  display: flex;
  align-items: center;
}

#app .price {
  color: #f40;
  margin-right: 5px;
}

#app .accounts {
  width: 70px;
  height: 30px;
  color: rgba(255, 255, 255, 0.8);
  background-color: #f40;
  border: none;
  border-radius: 15px;
  font-size: 8px;
}
</style>