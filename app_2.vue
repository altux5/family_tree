<template>
  <div class="flex-container">
    <div>
      <div id="headline">
      <h2>Family Tree</h2><h5>Add a Child to the Tree!</h5></div>
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
  <li class="linav"><a>Address <input v-model="Address" type="text"></a> </li>
  <li class="linav"><a>Deceased? <input type="checkbox" v-model="isDeceased"></a>
  <li class="linav" v-show="isDeceased"><a>Date of death <input v-model="deathDate" type="text" placeholder="__day__/_month_/___year___"></a></li>
  <li class="linav" v-show="isDeceased"><a>Graveyard Address <input v-model="graveyardAddress" type="text"></a></li>
    <li class="linav"><a>Add Picture url<input v-model="Picture" type="text"></a> </li>
  <button @click="onAddNewChild()">Add the Child!</button>
</ul>
        </div>
    </div>

    <div class="tree"></div>
    <div id="fyi"><h6>red=deceased*</h6></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      birthDate: "",
      Address: "",
      graveyardAdress: "",
      deathDate: "",
      childName: "",
      childSurName: "",
      isChecked1: false,
      isDeceased: false,
      selectedParent: "",
      parents: [],
      Picture: "",
      data: [
        {
          name: "Baba",
          surname: "soyad",
          deceased: true,
          adress: "Itu_TEqnoKentxdé",
          graveyard: "Zincirlikuyu",
          dateofbirth: "17/02/1899",
          dateofdeath: "22/11/2009",
          img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",

          wife: {
            name: "Anne",
            surname: "soyad",
            deceased: true,
            adress: "Itu_TEqnoKentxdé",
            graveyard: "Zincirlikuyu",
            dateofbirth: "27/12/1909",
            dateofdeath: "22/11/2009",
            img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
          },
          children: [
            {
              name: "Çocuk 1",
              surname: "soyad",
              deceased: true,
              adress: "Itu_TEqnoKentx",
              graveyard: "Zincirlikuyu",
              dateofbirth: "13/06/1932",
              dateofdeath: "22/11/2009",
              img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",

              wife: {
                name: "Gelin 1",
                surname: "soyad",
                deceased: false,
                adress: "Itu_TEqnoKentx",
                graveyard: "Zincirlikuyu",
                dateofbirth: "07/10/1937",
                dateofdeath: "-",
                img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
              },
              children: [
                {
                  name: "Torun 1",
                  surname: "soyad",
                  deceased: false,
                  adress: "Itu_TEqnoKentx",
                  graveyard: "Zincirlikuyu",
                  dateofbirth: "07/10/1957",
                  dateofdeath: "-",
                  img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
  
                  wife: {
                    name: "Gelin 2",
                    surname: "soyad",
                    deceased: false,
                    adress: "Itu_TEqnoKentx",
                    graveyard: "Zincirlikuyu",
                    dateofbirth: "14/08/1958",
                    dateofdeath: "-",
                    img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
                  },
                  children: [
                    {
                      name: "torun",
                      surname: "soyad",
                      deceased: false,
                      adress: "Itu_TEqnoKentxdé",
                      graveyard: "Zincirlikuyu",
                      dateofbirth: "30/03/1979",
                      dateofdeath: "-",
                      img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
                  
                      wife: {
                        name: "gelin",
                        surname: "soyad",
                        deceased: false,
                        adress: "Itu_TEqnoKentx",
                        graveyard: "Zincirlikuyu",
                        dateofbirth: "30/03/1979",
                        dateofdeath: "-",
                        img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
                      }
                    }
                  ]
                },
                {
                  name: "Torun 2",
                  surname: "soyad",
                  deceased: true,
                  adress: "Itu_TEqnoKentxdé",
                  graveyard: "Zincirlikuyu",
                  dateofbirth: "30/03/1979",
                  dateofdeath: "22/11/2009",
                  img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",

                }
              ]
            },
            {
              name: "Çocuk 2",
              surname: "soyad",
              deceased: false,
              adress: "Itu_TEqnoKentx",
              graveyard: "Zincirlikuyu",
              dateofbirth: "30/03/1979",
              dateofdeath: "-",
              img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
    
              wife: {
                name: "Damat 1",
                surname: "soyad",
                deceased: true,
                adress: "Itu_TEqnoKentx",
                graveyard: "Zincirlikuyu",
                dateofbirth: "30/03/1979",
                dateofdeath: "22/11/2009",
                img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",

              },
              children: [
                {
                  name: "Torun 3",
                  surname: "soyad",
                  deceased: false,
                  adress: "Itu_TEqnoKentx",
                  graveyard: "Zincirlikuyu",
                  dateofbirth: "30/03/1979",
                  dateofdeath: "-",
                  img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
             
                  wife: {
                    name: "Gelin 3",
                    surname: "soyad",
                    deceased: false,
                    adress: "Itu_TEqnoKentx",
                    graveyard: "Zincirlikuyu",
                    dateofbirth: "30/03/1979",
                    dateofdeath: "-",
                    img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
                  }
                }
              ]
            },
            {
              name: "Çocuk 3",
              surname: "soyad",
              deceased: false,
              adress: "Itu_TEqnoKentx",
              graveyard: "Zincirlikuyu",
              dateofbirth: "30/03/1979",
              dateofdeath: "-",
              img: "http://ozelsozler.com/foto/mustafa-kemal-ataturk.jpg",
     
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
            data[i].children.push({
              name: _self.childName, 
              deceased: _self.isDeceased, 
              surname: _self.childSurName,
              adress: _self.Address,
              graveyard:_self.graveyardAddress,
              dateofbirth:_self.birthDate,
              dateofdeath:_self.deathDate,
              img:_self.Picture});
          } else {
            data[i].children.push({
              name: _self.childName, 
              deceased: _self.isDeceased, 
              surname: _self.childSurName,
              adress: _self.Address,
              graveyard:_self.graveyardAddress,
              dateofbirth:_self.birthDate,
              dateofdeath:_self.deathDate,
              img:_self.Picture});
                    
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
          if(!data[i].deceased){
          html += "<a>" + "<b>"+ + data[i].name + " " + data[i].surname + "</b>" +"<p class='birthdate'>" + data[i].dateofbirth + "--" + data[i].dateofdeath + "</p>" + "<img src='" + data[i].img + "' alt='picture'>" +
          "<br>" +"Adress:" + data[i].adress +"Adress:" + "</a>";
          }
          else{
            html += "<a class='deceased'>"+ "<b>" + data[i].name + " "+ data[i].surname + "</b>" +"<p class='birthdate'>" + data[i].dateofbirth + " -- " + data[i].dateofdeath + "</p>" + "<img src='" + data[i].img + "' alt='picture'>" + "<br>" +"Adress:"  + data[i].adress + "<br>"+ "graveyard adress:" + data[i].graveyard + "</a>"
          }
          if (typeof data[i].wife !== "undefined") {
            if(!data[i].wife.deceased){
            html += "<a class='wife'>" + "<b>" + data[i].wife.name + " "+ data[i].wife.surname + "</b>" +"<p class='birthdate'>" + data[i].wife.dateofbirth + "--" + data[i].wife.dateofdeath  + "</p>" + "<img src='" + data[i].img + "' alt='picture'>" + "<br>" +"Adress:" + data[i].wife.adress + "</a>";
            }
            else{
            html += "<a class='deceasedWife'>" + "<b>" + data[i].wife.name + " " + data[i].wife.surname + "</b>" +"<p class='birthdate'>" + data[i].wife.dateofbirth + " -- " + data[i].wife.dateofdeath + "</p>" + "<img src='" + data[i].img + "' alt='picture'>" + "<br>" +"Adress:" + data[i].wife.adress + "<br>"+ "graveyard adress:" + data[i].wife.graveyard + "</a>";
            }
          }
          html += this.buildList(data[i].children, isSub); // Submenu found. Calling recursively same method (and wrapping it in a div)
        } else if(!data[i].deceased){
          html += "<a>" + "<b>" + data[i].name + " "+ data[i].surname + "</b>" +"<p class='birthdate'>" + data[i].dateofbirth + "--" + data[i].dateofdeath + "</p>" + "<img src='" + data[i].img + "' alt='picture'>" + "<br>" +"Adress:" + data[i].adress +  "</a>";
        }
        else{
          html += "<a class='deceased'>" + "<b>" + data[i].name + " "+ data[i].surname + "</b>" +"<p class='birthdate'>" + data[i].dateofbirth + " -- " + data[i].dateofdeath + "</p>" + "<img src='" + data[i].img + "' alt='picture'>" + "<br>" +"Adress:" + data[i].adress  + "<br>" +"graveyard adress:" + data[i].graveyard +  "</a>";
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

}.birthdate{
  font-family: Verdana;
  font-size: 75.7%;
  background-color: black;
  color: white;

}
 

#fyi{
  font-family: Verdana;
  font-size: 100%;
  color: black;

}


input{
  width: 200px;
  height: 16px;
}
select{
  width: 150px;
  height: 16px;
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

   
}



.wife {
  margin-left: 10px;
}
.deceasedWife{
  margin-left: 10px;
  background-color: rgb(117, 25, 25);
}
.ulnav {
  list-style-type: none;
  margin: 0;
  padding: 0;
  width: 250px;
  background-color: #f1f1f1;

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
.deceased{
  background-color: rgb(117, 25, 25);
}
b {
  color: rgb(235, 172, 0);
  font-size: 120%;
}
</style>
