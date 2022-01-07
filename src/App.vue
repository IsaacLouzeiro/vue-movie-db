<template>
    <nav>
        <div>
            <router-link to="/">
                <h1>Lou<span>Z</span></h1>
            </router-link>
        </div>
    </nav>
    <main>
        <router-view />
    </main>
    <footer>
        <div>
            <span class="rights"><h1>Lou<span>Z</span></h1><span>©  All rights reserved</span></span>

            <span class="by">By Isaac Louzeiro <a href="https://github.com/IsaacLouzeiro" target="_blank"><font-awesome-icon class="icon" :icon="['fab', 'github-square']" /></a> <a href="https://www.linkedin.com/in/isaac-louzeiro" target="_blank"><font-awesome-icon class="icon" :icon="['fab', 'linkedin']" /></a></span>
        </div>
    </footer>
</template>

<script>
export default {
    name: 'App'
}
</script>

<style lang="scss">
    //colors
    $color1: #357ded;
    $color2: #151515;
    $color3: #32e875;
    $color4: #e1e5ee;
    $color5: #5438dc;

    * { 
        margin: 0; 
        padding: 0; 
        box-sizing: border-box; 
        font-family: 'Trebuchet MS', sans-serif;

        &::selection {
            background: transparentsize($color1, 0.5);
        }
    }

    html, body {
        height: 100%;
    }

    body {
        background-color: $color4;
    }

    #app {
        height: 100%;
        display: flex;
        flex-wrap: nowrap;
        flex-direction: column;
    }

    a {
        text-decoration: none;
    }

    nav {
        background-color: $color1;
        box-shadow: 0px 0px 6px rgba(0,0,0,0.1);
        div {
            max-width: 1400px;
            margin: auto;
            display: flex;
            align-items: center;
            justify-content: start;
            padding: 10px 16px;
    
            h1 {
                color: $color3;
                font-size: 2em;
    
                span {
                    color: $color4;
                }
            }
        }

    }

    footer {
        background-color: $color1;
        margin-top: auto;
        padding: 20px 16px;

        div {
            width: 100%;
            max-width: 1400px;
            margin: auto;

            .rights {
                display: block;
                text-align: center;
                h1 {
                    color: $color3;
                    font-size: 1.5em;
                    display: inline-block;
                    margin-right: 10px;
    
                    span {
                        color: $color4;
                    }
                }
                
                span {
                    font-size: 1.2em;
                    color: $color4;
                }
            }
    
            .by {
                color: $color4;
                font-size: 1em;
                display: block;
                display: flex;
                justify-content: end;
                align-items: center;
                margin-top: 15px;
    
                a {
                    color: $color3;
                    display: inline-block;
                    margin-left: 10px;

                    &:hover {
                        color: $color5;
                    }
                }
    
                .icon {
                    font-size: 1.5em;
                }
            }
        }

    }
</style>
