<template>
  <div class="container">
    <header class="nav-header" :class="{'scroll' :scroll}">
      <a class="logo">LOGO</a>
      <ul>
        <li><a class="active">Home</a></li>
        <li><a>About</a></li>
      </ul>
    </header>
    <div class="box" :class="{'scroll' : scroll}" >
      <ul class=img-list >
        <li v-for="n in totalImg" :key="n" :style="img(n)" :class="{'active' : displayImg==n}"></li>
      </ul>
      <p>Some text here...</p>
      <div class="mouseTips">
        <div align="center">
          <span style="color: #fff;"><b>scroll down</b></span>
          <i style="color: #fff;margin:10px" class="fa-solid fa-angles-down fa-2xl"></i>
        </div>
      </div>
    </div>
    <div class="content">

    </div>
  </div>
</template>

<style lang="scss">
.nav-header{
  position: fixed;
  z-index: 1000;
  width: 100%;
  display: flex;
  .logo{
    transition: all 0.5s;
    text-transform:uppercase;
    text-decoration: none;
    color: white;
    font-size: 3rem;
    font-weight: 700;
    margin-right: auto;
    margin-left: 30px;
    padding-top:15px;
    padding-bottom:15px;
  }
  
  ul{
    list-style: none;
    display:flex;
    align-items: center;
    margin-right: 30px;

    li{
      padding-left: 15px;
      padding-right: 15px;
      a{
        transition: all 0.5s;
        text-decoration:none;
        color: white;
        font-size:1.2rem;
        padding:15px;
        border-radius: 100px;
        text-shadow: 0.1em 0.1em 0.05em #333;
      }
      a:hover,a.active{
        transition: all 0.5s;
        color:gray;
        background-color:white;
        text-shadow: none;
      }
    }
  }

}
.nav-header.scroll{
  background-color:rgba(255, 255, 255, 0.9);
  .logo{
    color: #696773;
  }
  ul{
    li{
      a{
        color: #272727;
        text-shadow: 0.1em 0.1em 0.05em rgba(255, 255, 255, 0);
      }
      a:hover,a.active{
        color:white;
        background-color:#272727;
        text-shadow: none;
      }
    }
  }

}
.container{
  position: relative;
  height: 100vh;
  width: 100%;
  background-color:rgb(255, 255, 255);
}

.img-list{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color:#272727;
  top:55%;
  left: 50%;
  list-style: none;
  transform: translate(-50%,-55%);
  transition: all 0.5s;
  overflow: hidden;
  li{
    position: absolute;
    width: 100%;
    height: 100%;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    transition: all 1s;
    opacity: 0;
    transform: scale(1.1)
  }
  li.active{
    opacity: 1;
    animation-name:imgScale;
    animation-duration:3s;
    animation-timing-function: linear;
  }
}
@keyframes imgScale{
  0%{
    transform: scale(1)
  }
  100%{
    transform: scale(1.1)
  }
}

.scroll .img-list{
    width:80vw;
    height:400px;
}
.box{
  height:100vh;
  width:100%;
  p{
    z-index: 2;
    position: absolute;
    color: white;
    font-size: 5vw;
    top:45%;
    left: 15%;
    text-shadow: 5px 5px 0em rgba(48, 48, 48, 0.836);
    overflow: hidden;
    animation-name:title;
    animation-duration: 3s;
    animation-iteration-count: 1;
    white-space:nowrap;
    width: 100%;
  }
  @keyframes title{
    0%{
      width: 0;
    }
    100%{
      width: 100%;
    }
  }
  .mouseTips{
    position: absolute;
    bottom:10px;
    right: calc(50% - 50px);
    height: 100px;
    width: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    animation-name:mouseTipsA;
    animation-duration:0.8s;
    animation-iteration-count: infinite;
    animation-direction:alternate;

    }
    @keyframes mouseTipsA{
      0%{
        transform:translateY(0)
      }
      100%{
        transform:translateY(-10px)
      }
    }
}


.content{
  height: 100%;
  width: 100%;
  background-color:#EFF1F3;
}
</style>

<script>
export default {
  created(){
    window.addEventListener("scroll",this.handleScroll)
  },
  data(){ 
    return { 
      scroll:false,
      displayImg:1,
      totalImg:5
    }
  },
  mounted(){
    setInterval(this.changeImg,3000)
  },
  methods: {
    handleScroll(){
      this.scroll = (window.scrollY > 0)
    },
    img(n){
      return {
        backgroundImage:`url(https://picsum.photos/1920/1080?random=${n})`
      }
    },
    changeImg(){
      if(this.displayImg==this.totalImg){
        this.displayImg=1
      }else{
        this.displayImg++
      }
    },
  }
}
</script>
