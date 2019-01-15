<template>
    <div class="hello">
        <form>
            <div class="form-group">
                <input class="form-control" v-model="message" v-on:keyup.prevent="handler" placeholder="Write something">
                <div class="tooltip">
                    <p v-for="tip in tips" @click="setTip">{{ tip }}</p>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
  export default {
    name: 'Tip',
    data() {
      return {
        message: '',
        startTip: 3,
        url: 'http://localhost:8081',
        tips: [],
        limit: 6
      };
    },
    methods: {
      getUrl(_url, _data) {
        const url = new URL(_url),
            params = {data: _data};
        Object.keys(params).forEach(key => url.searchParams.append(key, params[key]));
        return url;
      },
      handler(e) {
        this.tips = [];
        if (this.message.length >= this.startTip) {
          fetch(this.getUrl(this.url, this.message)).then((response) => {
            return response.json();
          }).then((response) => {
            for (let i = 0; i < response.length; i++) {
              if (i === this.limit) {
                break;
              }
              this.tips.push(response[i].text)
            }
          }).catch(alert);
        }
      },
      setTip (e) {
        this.message = e.target.innerHTML
        this.tips = []
      }
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    .form-control {
        display: block;
        width: 100%;
        padding: .375rem .75rem;
        font-size: 1rem;
        line-height: 1.5;
        color: #495057;
        background-color: #fff;
        background-clip: padding-box;
        border: 1px solid #ced4da;
        border-radius: .25rem;
        transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out;
    }
    .tooltip {
        text-align: left;
    }
    .tooltip p {
        cursor: pointer;
        border:1px solid #ddd;
        padding: 8px;
    }
</style>
