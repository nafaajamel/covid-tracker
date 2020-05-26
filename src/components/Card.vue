<template>
  <md-card :class="'card' +  getClassName" md-with-hover>
    <md-ripple>
      <md-card-header>
        <div class="md-title">{{title}}</div>
        <div class="md-subhead">
          <ICountUp :delay="4000" 
           :endVal="subTitle || 0" 
           :options="countOptions"
          />
        </div>
      </md-card-header>
      <md-card-content>{{description}}</md-card-content>
    </md-ripple>
  </md-card>
</template>
<script>
import ICountUp from "vue-countup-v2";
export default {
  name: "Card",
  props: {
    title: String,
    subTitle: Number,
    description: String
  },
  components: { ICountUp },
  data(){
    return {
      countOptions:{
        separator:' '
      }
    }
  },
  computed: {
    getClassName() {
      let title = this.title.toLowerCase();
      return title === "infected"
        ? ` warning`
        : title === "recovered"
        ? ` sucess`
        : ` danger`;
    }
  }
};
</script>

<style scoped>
.card {
  margin: 15px 0;
}

.danger {
  border-bottom: 5px inset rgb(255, 0, 0) !important;
}
.danger .md-subhead {
  color: rgb(255, 0, 0);
}
.warning {
  border-bottom: 5px inset rgb(156, 140, 48);
}
.warning .md-subhead {
  color: rgb(156, 140, 48);
}
.sucess {
  border-bottom: 5px inset rgb(1, 255, 1);
}
.sucess .md-subhead {
  color: rgb(1, 255, 1);
}
</style>

