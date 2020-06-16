<template>
  <div>
    <div class="goods" v-for="(goods,row) in goodsList" :key="goods.id">
      <div class="title">{{ goods.title}}</div>
      <ul class="type-list">
        <li
          class="type"
          v-for="(list,i) in goods.typeList"
          :key="i"
          :class="{
            active: goods.index === i 
        }"
          @click="handleClick(i,goods,list,row)"
        >{{ list }}</li>
      </ul>
    </div>
    <div class="choose-type">
      <div>已选条件：</div>
      <span class="no-goods" v-if="!showFlag">暂时没有选择过滤的条件</span>
      <ul class="filter-list" v-else>
        <li v-for="(goods,index) in filterList" :key="index">{{ goods }}
          <span class="delete-goods" @click="deleteGoods(index)">x</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      goodsList: [
        {
          title: "上装",
          typeList: [
            "全部",
            "针织衫",
            "毛呢外套",
            "T恤",
            "羽绒服",
            "棉衣",
            "卫衣",
            "风衣"
          ],
          id: 1
        },
        {
          title: "裤装",
          typeList: [
            "全部",
            "牛仔裤",
            "小脚/铅笔裤",
            "休闲裤",
            "打底裤",
            "哈伦裤"
          ],
          id: 2
        },
        {
          title: "裙装",
          typeList: ["全部", "连衣裙", "半身裙", "长袖连衣裙", "中长款连衣裙"],
          id: 3
        }
      ],
      filterList: {},
      showFlag: false
    };
  },
  created() {
    this.goodsList.forEach(item => this.$set(item, "index", 0));
  },
  methods: {
    handleClick(i,goods,list,row){
      this.showFlag = true;
      goods.index = i;
      if(list == '全部'){
        this.$delete(this.filterList,row);
        this.checkShowFilter();
        return;
      };
      this.$set(this.filterList,row,list);
    },
    deleteGoods(key){
      this.$delete(this.filterList,key)
      this.goodsList[key].index = 0;
      this.checkShowFilter();
    },
    checkShowFilter(){
      const a = JSON.stringify(this.filterList)
      this.showFlag = a !== '{}'
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
  padding: 0;
}

ul,
li {
  list-style: none;
}

#app {
  width: 550px;
  margin: 80px auto;
  padding: 5px 15px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 12px;
  color: #666;
}

#app .goods {
  display: flex;
  align-items: center;
  border-bottom: 1px dashed #eee;
  text-indent: 2em;
}

#app .goods:last-child {
  border-bottom: none;
}

#app .goods .type-list {
  display: flex;
  text-indent: 0;
}

#app .goods .type-list .type {
  margin: 15px 7px;
  padding: 5px 6px;
  border-radius: 3px;
  color: #039;
  cursor: pointer;
}

#app .goods .type-list .type:hover {
  color: #f60;
  background-color: #f3edc2;
}

#app .goods .type-list .type.active {
  color: #fff;
  background-color: #f60;
}

#app .choose-type {
  display: flex;
  align-items: center;
  font-weight: bold;
}

#app .choose-type .no-goods {
  color: #999;
  font-weight: normal;
  padding: 20px;
}

#app .choose-type .filter-list {
  display: flex;
  font-weight: normal;
}

#app .choose-type .filter-list li {
  margin: 15px 10px;
  padding: 5px 8px;
  border-radius: 3px;
  color: #fff;
  background-color: #f60;
  cursor: pointer;
}

#app .choose-type .filter-list li .delete-goods {
  opacity: 0.5;
}

#app .choose-type .filter-list li .delete-goods:hover {
  opacity: 1;
}
</style>
