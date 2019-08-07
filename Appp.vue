<template>
  <div>
    <select v-model="selectedParent">
      <option :value="item" :key="item" v-for="item in parents">{{item}}</option>
    </select>
    <input v-model="childName" type="text" style="width:200px" />
    <button @click="onAddNewChild()">Ekle</button>
    <div class="tree"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      childName: "",
      selectedParent: "",
      parents: [],
      data: [
        {
          name: "Baba",
          id:10,
          wife: {
            name: "Anne",
            id:11,
          },
          children: [
            {
              name: "Çocuk 1",
              id:20,
        
              wife: {
                name: "Gelin 1",
                id:21,
              },
              children: [
                {
                  name: "Torun 1",
                  id:50,
                
                  wife: {
                    name: "Gelin 2",
                    id:51,
                  },
                  children: [
                    {
                      name: "torun",
                      id:80,
               
                      wife: {
                        name: "gelin",
                        id:81,
                      }
                    }
                  ]
                },
                {
                  name: "Torun 2",
                  id:60,
                  
                }
              ]
            },
            {
              name: "Çocuk 2",
              id:30,
              wife: {
                name: "Damat 1",
                id:31,
              },
              children: [
                {
                  name: "Torun 3",
                  id:70,
                  wife: {
                    name: "Gelin 3",
                    id:71,
                  }
                }
              ]
            },
            {
              name: "Çocuk 3",
              id:40,
            }
          ]
        }
      ]
    };
  },
  
  methods: {
    getParents(node) {
      let data;
      if (!node) {
        data = this.data;
      } else {
        data = node;
      }
      data.forEach(d => {
        this.parents.push(d.name);
        if (d.children) {
          this.getParents(d.children);
        }
      });
    } , 
    onAddNewChild() {  
      this.addNewChild(this.data);
    },
    addNewChild(data, isSub) {
      let _self = this;
      for (let i = 0; i < data.length; i++) {
        if (_self.selectedParent === data[i].name) {
          if (!data[i].children) {
            data[i].children = [];
            data[i].children.push({name: _self.childName});

          } else {
            data[i].children.push({name: _self.childName});
          }
          _self.drawFamilyTree();
          return;
        }
        if (data[i].children) {
          _self.addNewChild(data[i].children, isSub);
        }
      }
      console.log(JSON.stringify(this.data));
    },

    buildList(data, isSub) {
      var html = isSub ? "<div>" : ""; // Wrap with div if true
      html += "<ul>";

     for (let i = 0; i < data.length; i++) {
            
        html += "<li>";
        if (typeof data[i].children !== "undefined") {
          html += "<a>" + data[i].name + "</a>"; 
  
          if (typeof data[i].wife !== "undefined") {
            html += "<a class='wife'>" + data[i].wife.name +  "</a>";
           
          }
        
          html += this.buildList(data[i].children, isSub); // Submenu found. Calling recursively same method (and wrapping it in a div)
          
        } else {
          html += "<a>" + data[i].name + "</a>";
        }
         data[i].id=i+1;
        html += "</li>";

      }
  
      html += "</ul>";
      html += isSub ? "</div>" : "";
      return html;
    },
    
    drawFamilyTree() {
      document.querySelector(".tree").innerHTML = this.buildList(
        this.data,
        false
      );
    }
  },
  mounted() {
    this.getParents();
    this.drawFamilyTree();
  }
};
</script>

<style>
* {
  margin: 0;
  padding:0;
  
}

.tree ul {
  padding-top: 20px;
  position: relative;

  transition: all 0.5s;
  -webkit-transition: all 0.5s;
  -moz-transition: all 0.5s;
}

.tree li {
  float: left;
  text-align: center;
  list-style-type: none;
  position: relative;
  padding: 20px 5px 0 5px;

  transition: all 0.5s;
  -webkit-transition: all 0.5s;
  -moz-transition: all 0.5s;
}

.tree li::before,
.tree li::after {
  content: "";
  position: absolute;
  top: 0;
  right: 50%;
  border-top: 1px solid #ccc;
  width: 50%;
  height: 20px;
}
.tree li::after {
  right: auto;
  left: 50%;
  border-left: 1px solid #ccc;
}

.tree li:only-child::after,
.tree li:only-child::before {
  display: none;
}

.tree li:only-child {
  padding-top: 0;
}

.tree li:first-child::before,
.tree li:last-child::after {
  border: 0 none;
}
.tree li:last-child::before {
  border-right: 1px solid #ccc;
  border-radius: 0 5px 0 0;
  -webkit-border-radius: 0 5px 0 0;
  -moz-border-radius: 0 5px 0 0;
}
.tree li:first-child::after {
  border-radius: 5px 0 0 0;
  -webkit-border-radius: 5px 0 0 0;
  -moz-border-radius: 5px 0 0 0;
}
.tree ul ul::before {
  content: "";
  position: absolute;
  top: 0;
  left: 50%;
  border-left: 1px solid #ccc;
  width: 0;
  height: 20px;
}

.tree li a {
  border: 1px solid #ccc;
  padding: 5px 10px;
  text-decoration: none;
  color: #666;
  font-family: arial, verdana, tahoma;
  font-size: 11px;
  display: inline-block;

  border-radius: 5px;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;

  transition: all 0.5s;
  -webkit-transition: all 0.5s;
  -moz-transition: all 0.5s;
}

.tree li a:hover,
.tree li a:hover + ul li a {
  background: #c8e4f8;
  color: #000;
  border: 1px solid #94a0b4;
}

.tree li a:hover + ul li::after,
.tree li a:hover + ul li::before,
.tree li a:hover + ul::before,
.tree li a:hover + ul ul::before {
  border-color: #94a0b4;
}

.wife {
  margin-left: 10px;
}
</style>
