<template>
    <div>
        <h1>{{title}}</h1>
        <div id="result">
            <div class="flex-container">
                <div class="groups" v-for="group in renderableGroups">
                    <div v-for="color in group">
                        <div class="ball" v-bind:style="{background: 'radial-gradient(circle at 33% 33%, ' + color + ', #000)'}"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ballDistribution',
  data() {
      return {
          title: 'Ball distribution',
          n: 3,
          groups: [
              [{yellow: 2},{red: 1}],
              [{yellow: 2},{red: 1}],
              [{blue: 3}]
          ]
    }
  },
  computed: {
      renderableGroups() {
         let renderableGroups = [];
         for (let i=0; i<this.groups.length; i++){
             let distribution = this.groups[i];
             renderableGroups[i] = [];
             for(let j=0; j<distribution.length; j++) {
                 let set = distribution[j];
                 for(let property1 in set)
                 {
                     if(set.hasOwnProperty(property1))
                         for(let count=0; count<set[property1]; count++)
                         renderableGroups[i].push(property1);
                 }
             }
         }
         return renderableGroups;
      }
  }
}
</script>

<style scoped>
    .flex-container {
        display: flex;
    }
    .groups {
        padding: 0 10px;
    }
    .groups:nth-child(even) {
        background: #EEEEEE;
    }
    .groups:nth-child(odd) {
        background: #E0E0E0;
    }
    .ball {
        display: inline-block;
        width: 100px;
        height: 100px;
        margin: 3px;
        border-radius: 50%;
        position: relative;
    }
    .ball:before {
        content: "";
        position: absolute;
        background: radial-gradient(circle at 50% 120%, rgba(255, 255, 255, 0.5), rgba(255, 255, 255, 0) 70%);
        border-radius: 50%;
        bottom: 2.5%;
        left: 5%;
        opacity: 0.6;
        height: 100%;
        width: 90%;
        filter: blur(5px);
        z-index: 2;
    }
    .ball:after {
        content: "";
        width: 100%;
        height: 100%;
        position: absolute;
        top: 5%;
        left: 10%;
        border-radius: 50%;
        background: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0.8) 14%, rgba(255, 255, 255, 0) 24%);
        transform: translateX(-80px) translateY(-90px) skewX(-20deg);
        filter: blur(10px);
    }
    h1, h2 {
        font-weight: normal;
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
</style>
