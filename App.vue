<template>
  <div class="flex-container">
    <div>
      <div id="headline">
      <h2>Family Tree</h2><br><h5>Add a Child to the Tree!</h5><br></div>
        <div>
          <ul class="ulnav">
  <li class="linav"><a class="active">Name of Parent:     <select v-model="selectedParent">
      <option :value="item" :key="item" v-for="item in parents">{{item}}</option>
    </select></a></li>
  <li class="linav"><a>Name of Child <input v-model="childName" type="text"></a> </li>
  <li class="linav"><a>Surname <input v-model="childSurName" type="text"></a></li>
  <li class="linav"><a>Married? <input type="checkbox" v-model="isChecked1"></a>
  <li class="linav" v-show="isChecked1"><a>Wife <input v-model="childsWife" type="text"></a> </li>
  <li class="linav"><a>Date of Birth <input v-model="birthDate" type="text" placeholder="__day__/_month_/___year___"></a></li>
  <li class="linav"><a>Address <input v-model="address" type="text"></a> </li>
  <li class="linav"><a>Deceased? <input type="checkbox" v-model="isChecked2"></a>
  <li class="linav" v-show="isChecked2"><a>Date of death <input v-model="deathDate" type="text" placeholder="__day__/_month_/___year___"></a></li>
  <li class="linav" v-show="isChecked2"><a>Graveyard Adress <input v-model="graveyardAddress" type="text"></a></li>
  <button @click="onAddNewChild()">Add the Child!</button>
</ul>
        </div>
    </div>

    <div class="tree"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      birthDate: "",
      graveyardAdress: "",
      deathDate: "",
      childName: "",
      childSurName: "",
      isChecked1: false,
      isChecked2: false,
      selectedParent: "",
      parents: [],
      data: [
        {
          name: "Baba",
          wife: {
            name: "Anne"
          },
          children: [
            {
              name: "Çocuk 1",
              wife: {
                name: "Gelin 1"
              },
              children: [
                {
                  name: "Torun 1",
                  wife: {
                    name: "Gelin 2"
                  },
                  children: [
                    {
                      name: "torun",
                      wife: {
                        name: "gelin"
                      }
                    }
                  ]
                },
                {
                  name: "Torun 2"
                }
              ]
            },
            {
              name: "Çocuk 2",
              wife: {
                name: "Damat 1"
              },
              children: [
                {
                  name: "Torun 3",
                  wife: {
                    name: "Gelin 3"
                  }
                }
              ]
            },
            {
              name: "Çocuk 3"
            }
          ]
        }
      ]
    };
  },
  /* v forla datayı bul elindeki childı ekle*/
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
    },
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
            html += "<a class='wife'>" + data[i].wife.name + "</a>";
          }
          html += this.buildList(data[i].children, isSub); // Submenu found. Calling recursively same method (and wrapping it in a div)
        } else {
          html += "<a>" + data[i].name + "</a>";
        }
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
  padding: 0;
}
#headline{
  font-family: Verdana;
  font-size: 75.7%;
  background-color: black;
  color: white;
  

}

input{
  width: 200px;
  height: 20px;
}
select{
  width: 150px;
  height: 20px;
}

.flex-container {
  display:flex;
}


.flex-container > div {
  background-color: #f1f1f1;
  padding: 5px;
  
  text-align: center;

  font-size: 30px;
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
.ulnav {
  list-style-type: none;
  margin: 0;
  padding: 0;
  width: 250px;
  background-color: #f1f1f1;
  position: fixed;
  height: 100%;
  overflow: auto;
  font-size: 80%;
  font-family: verdana;
}

.linav a {
  display: block;
  color: #000;
  padding: 8px 16px;
  text-decoration: none;
}

.linav a.active {
  background-color: #4CAF50;
  color: white;
}

.linav a:hover:not(.active) {
  background-color: #555;
  color: white;
}
</style>