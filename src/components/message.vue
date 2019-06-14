<template>
  <div class="col-md-6 col-lg-4">
    <div class="message-lists">
      <div class="message-group" v-for="(data,index) in data" v-bind:key="index" ref="msg" v-bind:name="data.message">
        <div class="photo-section" >
          <div class="vertical-line" ref="Line"></div>
          <div class="photo">
            <div class="frame">
              <img v-bind:src="data.photo">
            </div>
          </div>
        </div>
        <div class="content">
          <h4 class="text-muted">{{data.first_name+" "+data.last_name}}</h4>
          <h5 class="message" ref="message">{{data.message}}</h5>
          <h5 v-html="data.html" class="font-weight-bold text-muted"></h5>
          <div class="note" v-if="data.note">
            <p class="text-muted font-weight-bold">{{data.note}}</p>
          </div>
          <span class="text-muted font-weight-bold font-italic" v-if="data.date_time">{{data.date_time}}</span>
          <span class="text-muted font-weight-bold font-italic" v-else>-</span>
          <div class="item" v-for="(item,i) in data.items" v-bind:key="index" ref="status" v-bind:name="item.status">
            <h5 class="item-message">{{item.message}}</h5>
            <div class="item-status">
              <h5>{{item.status}}</h5>
            </div>
            <span class="text-muted font-weight-bold font-italic">{{item.date_time}}</span>
            <div class="horizontal-line"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'jojonomic-test',
  props: ["data"],
  mounted() {
    this.controlDOM()
  },
  methods: {
    controlDOM() {
      this.$refs.msg.map((res,i)=>{
        var message = res.attributes.name.value;

        if(message === "Transaction submitted") {
          res.firstChild.lastChild.firstChild.style.backgroundColor = "#fbc33d"
          res.firstChild.firstChild.style.backgroundColor = "#fbc33d"
          res.lastChild.childNodes[1].style.color = "#fbc33d"
        } else if(message === "On approve") {
          res.firstChild.lastChild.firstChild.style.backgroundColor = "#fbc33d"
          res.firstChild.firstChild.style.backgroundColor = "#fbc33d"
          res.lastChild.childNodes[1].style.color = "#fbc33d"
        } else if(message === "Transaction approved") {
          res.firstChild.lastChild.firstChild.style.backgroundColor = "#00a5ff"
          res.firstChild.firstChild.style.backgroundColor = "#00a5ff"
          res.lastChild.childNodes[1].style.color = "#00a5ff"
        } else {
          res.firstChild.lastChild.firstChild.style.backgroundColor = "#6c757d"
          res.firstChild.firstChild.style.backgroundColor = "#6c757d"
          res.lastChild.childNodes[1].style.color = "#6c757d"
        }
      })

      this.$refs.status.map((res,i)=>{
        var status = res.attributes.name.value;

        if(status === "approved") {
          res.lastChild.style.backgroundColor = "#00a5ff"
          res.firstChild.style.color = "#00a5ff"
          res.childNodes[1].style.backgroundColor = "#00a5ff"
          res.style.borderColor = "#00a5ff"
        } else {
          res.lastChild.style.backgroundColor = "#fbc33d"
          res.firstChild.style.color = "#fbc33d"
          res.childNodes[1].style.backgroundColor = "#fbc33d"
          res.style.borderColor = "#fbc33d"
        }
      })
    }
  }
}
</script>

<style>
  body {
    margin: 0;
  }

  p,h4 {
    margin: 0 !important;
  }

  .photo-section {
    text-align: center;
    margin-right: 1rem;
    position: relative;
  }

  .photo {
  }

  .frame {
    width: 100px;
    height: 100px;
    padding: 5px;
    border-radius: 50%;
    display: flex;
  }

  .frame img {
    width: 100%;
    border: 5px solid #fff;
    border-radius: 50%;
  }

  .message-group {
    display: flex;
  }

  .note {
    background-color: #e9e9e9;
    border-radius: 5px;
    padding: 10px;
  }

  .content {
    padding-bottom: 20px;

  }

  .vertical-line {
    width: 8px;
    height: 100%;
    display: inline-block;
    position: absolute;
    left: 50%;
    top: 0;
    transform: translate(-50%,0);
    z-index: -1;
  }

  .horizontal-line {
    width: 100%;
    height: 8px;
    display: inline-block;
    position: absolute;
    top: 20%;
    left: -72px;
    z-index: -2;
  }

  .item {
    border: 2px solid transparent;
    border-radius: 5px;
    padding: 10px;
    margin: 20px 0;
    position: relative;
    background-color: #fff;
  }

  .item-status {
    border-radius: 5px;
    padding: 3px 20px;
    color: #fff;
    font-weight: bold;
  }

</style>