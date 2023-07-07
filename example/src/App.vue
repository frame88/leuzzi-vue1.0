<!-- eslint-disable vue/attributes-order -->
<template>
    <div id="app">
        <div id="menu" style="display: flex; justify-content: center">
            <li data-menuanchor="page1" class="active"><a href="#page1">Chi sono</a></li>
            <li data-menuanchor="page2"><a href="#page2">Crea il tuo menu</a></li>
            <li data-menuanchor="page3"><a href="#page3">Siti attivi</a></li>
        </div>
        <!-- <ul class="actions">
            <li>
                <a class="actions-button" href="#" rel="noopener" @click="addSection">Add section</a>
            </li>
            <li>
                <a class="actions-button" href="#" rel="noopener" @click="removeSection">Remove section</a>
            </li>
            <li>
                <a class="actions-button" href="#" rel="noopener" @click="toggleNavigation">Toggle nav</a>
            </li>
            <li>
                <a class="actions-button" href="#" rel="noopener" @click="toggleScrollbar">Toggle scrollBar</a>
            </li>
        </ul> -->

        <full-page :options="options" id="fullpage" ref="fullpage">
            <!-- 1pagina -->
            <div class="section">
              <div style="text-align: center">
                <img src="../src/assets/img/newlogo.png" alt="logo Leuzzi">
              </div>
              <div style="text-align: center">
                  <h4 class="bold" style="font-size: 2em">Francesco Leuzzi</h4>
                  <p style="margin: 2rem;">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Recusandae, sunt nisi animi at distinctio eum
                      soluta dolor voluptas cupiditate quia officiis, harum dolore maiores quod mollitia. Illo nemo ex
                      temporibus!
                  </p>
                  <p class="mt1"><strong>Se hai bisogno di metterti in contatto con me, puoi mandarmi una mail all'indirizzo</strong><a class="block" href="mailto:fleuzzi97@gmail.com">fleuzzi97@gmail.com</a></p>
                  <a href="https://www.linkedin.com/in/francesco-leuzzi-5497a8221/?originalSubdomain=it" target="_blank">
                      <h2><i class="fa-brands fa-linkedin"></i></h2>
                  </a>
              </div>
            </div>

            <!-- 2pagina -->
            <div class="section makeurmenu">
                <div class="slide">
                  <h3>Menu</h3>
                  <div style="margin: 2rem; padding:1rem; color:white; background-color: rgba(0, 0, 0, 0.664); border-radius: 5px">
                    <span>Gli esempi seguenti si pongono l’obbiettivo di creare un’idea quanto più concreta di quello che sarà poi il menù finale, ma possono essere personalizzati in ogni loro aspetto e funzione in base alle necessità e ai gusti del cliente.</span>
                  </div>
                </div>
                <div class="slide" >
                  <div style="text-align: center; color: white">
                    <h3>Unus</h3>
                    <span>clicca sul titolo per visualizzare il menu</span>
                  </div>
                </div>
                <div class="slide">
                  <div style="text-align: center; color: white">
                    <h3>Duo</h3>
                    <span>clicca sul titolo per visualizzare il menu</span>
                  </div>
                </div>
                <div class="slide">
                  <div style="text-align: center; color: white">
                    <h3>Tribus</h3>
                    <span>Gli esempi seguenti si pongono l’obbiettivo di creare un’idea quanto più concreta di quello che sarà poi il menù finale, ma possono essere personalizzati in ogni loro aspetto e funzione in base alle necessità e ai gusti del cliente.</span> 
                  </div>
                </div>
              </div>

            <!-- 3pagina -->
            <div class="section website">
                <h3>Siti attivi</h3>
            </div>

        </full-page>
    </div>
</template>

<script>

// Optional. When using fullpage extensions
// import './fullpage.scrollHorizontally.min'

  export default {
    name: 'App',
    data () {
      return {
        options: {
          licenseKey: 'YOUR_KEY_HERE',
          afterLoad: this.afterLoad,
          scrollOverflow: true,
          scrollBar: false,
          menu: '#menu',
          navigation: true,
          anchors: ['page1', 'page2', 'page3', 'page4'],
          sectionsColor: ['white', '#ff5f45', '#0798ec', '#fec401', '#1bcee6', '#ee1a59', '#2c3e4f', '#ba5be9', '#b4b8ab']
        }
      }
    },
    methods: {

      afterLoad () {
        console.log('After load')
      },

      addSection (e) {
        e.preventDefault()
        var newSectionNumber = document.querySelectorAll('.fp-section').length + 1

        // creating the section div
        var section = document.createElement('div')
        section.className = 'section'
        section.innerHTML = `<h3>Section ${newSectionNumber}</h3>`

        // adding section
        document.querySelector('#fullpage').appendChild(section)

        // creating the section menu element
        var sectionMenuItem = document.createElement('li')
        sectionMenuItem.setAttribute('data-menuanchor', 'page' + newSectionNumber)
        sectionMenuItem.innerHTML = `<a href="#page${newSectionNumber}">Section${newSectionNumber}</a>`

        // adding it to the sections menu
        var sectionsMenuItems = document.querySelector('#menu')
        sectionsMenuItems.appendChild(sectionMenuItem)

        // adding anchor for the section
        this.options.anchors.push(`page${newSectionNumber}`)

        // we have to call `update` manually as DOM changes won't fire updates
        // requires the use of the attribute ref="fullpage" on the
        // component element, in this case, <full-page>
        // ideally, use an ID element for that element too
        this.$refs.fullpage.build()
      },

      removeSection () {
        var sections = document.querySelector('#fullpage').querySelectorAll('.fp-section')
        var lastSection = sections[sections.length - 1]

        // removing the last section
        lastSection.parentNode.removeChild(lastSection)

        // removing the last anchor
        this.options.anchors.pop();

        // removing the last item on the sections menu
        var sectionsMenuItems = document.querySelectorAll('#menu li')
        var lastItem = sectionsMenuItems[sectionsMenuItems.length - 1]
        lastItem.parentNode.removeChild(lastItem)
      },

      toggleNavigation () {
        this.options.navigation = !this.options.navigation
      },

      toggleScrollbar () {
        console.log('Changing scrollbar...')
        this.options.scrollBar = !this.options.scrollBar
      }
    }
  }
</script>

<style>
    ul {
        list-style-type: none;
        padding: 0;
    }
    li {
        display: inline-block;
        margin: 0 10px;
    }
    a {
         color: #5296A5;
         font-weight: 600; 
    }

    img {
      width: 100px;
      margin-bottom: 2rem;
    }

    #menu {
      background-color: rgba(0, 0, 0, 0.341);
      height: 7vh;
      display: flex;
      align-items: center;
      width: 100%
    }
    
    .makeurmenu {
      background-image: url('../src/assets/img/dwinanda-nurhanif-mujito-pKT5Mg16w_w-unsplash.jpg');
      background-position:bottom;
      background-size: cover;
    }
    
    .website {
      background-image: url('../src/assets/img/austin-neill-5CusMrOVwqI-unsplash.jpg');
      background-position: center;
      background-size: cover;
    }
</style>
