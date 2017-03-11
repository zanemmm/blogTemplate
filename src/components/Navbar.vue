<template lang="html">
  <div class="navbar">
    <header>
      <img v-on:hover="" :src="src" :alt="alt">
      <h1>{{name}}</h1>
      <h2>{{intro}}</h2>
    </header>
    <nav>
      <ul>
        <li :class="{active: menu.id === activeId}"
        v-for="menu in menus"
        v-on:click="selected(menu.id)">{{menu.name}}</li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  name: 'navbar',
  methods: {
    selected: function (id) {
        this.activeId = id;
        this.$parent.$emit('menuSelected', id);
    }
  },
  data () {
    return {
      src: 'https://avatars0.githubusercontent.com/u/23761319?v=3&s=460',
      alt: 'logo',
      name: 'zane',
      intro: 'intro',
      activeId: 1,
      menus: [
        {
          id: 1,
          url: './category/1',
          name: '全部文章',
        },
        {
          id: 2,
          url: './category/2',
          name: '分类一',
        },
        {
          id: 3,
          url: './category/3',
          name: '分类二',
        },
        {
          id: 4,
          url: './category/4',
          name: '分类三',
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
  $small: "(max-width: 479px)";
  $white: #EEE;
  $black: #222831;
  $gray:  #BBB;
  $size: 8px;
  $radius: 8px 0 0 8px;
  $menuTransition: transform ease .6s;
  .navbar {
    width: 250px;
    @media #{$small} {
      width: 40%;
    }
    color: $white;
    background-color: $black;
    header {
      padding: $size*2;
      text-align: center;
      img {
        display: block;
        margin: 0 auto;
        width: 50%;
        box-shadow: 0px 0px $size*2 $size/2 rgba(255,255,255,0.2);
        border-radius: 100%;
      }
    }
    nav {
      padding: $size*2 0;
      overflow: hidden;
      ul {
        display: flex;
        flex-direction: column;
        align-items: flex-end;
        padding: $size 0;
        overflow: hidden;
        list-style-type: none;
        li {
          margin: $size 0;
          width: 80%;
          height: $size*7;
          line-height: $size*7;
          text-align: center;
          color: $gray;
          background-color: #393E46;
          border-radius: $radius;
          transition: $menuTransition;
          cursor: pointer;
          box-shadow: 0px 0px $size 0px rgba(0,0,0,0.75);
        }
        li:hover:not(.active) {
          color: $white;
          transform: translateX(10%);
          transition: $menuTransition;
        }
        .active {
          position: relative;
          color: $black;
          background-color: $white;
          border-radius: $radius;
          transform: translateX(10%);
          transition: none;
        }
        .active:before {
          content: '';
          position: absolute;
          box-sizing: padding-box;
          top: -$size;
          right: calc(10% - 4px);
          width: $size;
          height: $size;
          background: transparent;
          border-radius: 0 0 $size 0;
          border-right: $size/2 solid $white;
          border-bottom: $size/2 solid $white;
        }
        .active:after {
          box-sizing: padding-box;
          position: absolute;
          bottom: -$size;
          right: calc(10% - 4px);
          width: $size;
          height: $size;
          content: '';
          background: transparent;
          border-radius: 0 $size 0 0;
          border-top: $size/2 solid $white;
          border-right: $size/2 solid $white;
        }
      }
    }
  }
</style>