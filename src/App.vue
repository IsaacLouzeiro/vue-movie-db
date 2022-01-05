<template>
  <nav>
    <router-link to="/">
        <h1>Lou<span>Z</span></h1>
    </router-link>
  </nav>
  <main>
    <router-view />
  </main>
</template>

<style lang="scss">
    //colors
    $color1: #04494F;
    $color2: #007A85;
    $color3: #64BEBF;
    $color4: #fff;
    $color5: #55B1BB;

    * { 
        margin: 0; 
        padding: 0; 
        box-sizing: border-box; 
        font-family: 'Trebuchet MS', sans-serif;

        &::selection {
            background: transparentsize($color1, 0.5);
        }
    }

    body {
        background-color: $color2;
    }

    a {
        text-decoration: none;
    }

    nav {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px 16px;
        background-color: $color1;
        box-shadow: 0px 0px 6px rgba(0,0,0,0.1);

        h1 {
            color: $color3;
            font-size: 2em;

            span {
                color: $color4;
            }
        }
    }
</style>
