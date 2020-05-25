<template>
    <v-app>
        <div v-for="block in blocks" :key="block.index" :class="block.type" @click.stop="openSettings(block.index)" :style="blockStyle(block)">
            <div v-if="block.type === 'fhh'" class="wrap">
                <h1 class="display-3 white--text my-5">{{ block.options.header }}</h1>
                <p class="headline white--text">{{ block.options.description }}</p>
            </div>
            <div v-if="block.type === 'col3'" class="wrap">
                <v-container>
                    <v-row>
                        <v-col cols="12" sm="4">
                            <h2><v-icon class="header-icon">mdi-{{ block.options.icon1 }}</v-icon>{{ block.options.header1 }}</h2>
                            <p>{{ block.options.description1 }}</p>
                        </v-col>
                        <v-col cols="12" sm="4">
                            <h2><v-icon class="header-icon">mdi-{{ block.options.icon2 }}</v-icon>{{ block.options.header2 }}</h2>
                            <p>{{ block.options.description2 }}</p>
                        </v-col>
                        <v-col cols="12" sm="4">
                            <h2><v-icon class="header-icon">mdi-{{ block.options.icon3 }}</v-icon>{{ block.options.header3 }}</h2>
                            <p>{{ block.options.description3 }}</p>
                        </v-col>
                    </v-row>
                </v-container>
            </div>
        </div>

        <Adder v-on:add-block="addBlockHandler" :fh="this.blocks.length === 0"></Adder>

        <v-navigation-drawer v-model="settingsList" fixed temporary>
            <v-container v-for="(value, name) in activeSettings" :key="name">
                <v-text-field :label="name" :placeholder="name" outlined v-model="activeSettings[name]" v-on:change="updateOption(name, value)"></v-text-field>
            </v-container>
        </v-navigation-drawer>
    </v-app>
</template>

<script>
    import Adder from './components/AdderBox';

    export default {
        name: 'App',

        components: {
            Adder,
        },

        data () {
            return {
                settingsList: false,
                activeSettings: {},
                activeBlock: null,
                blocks: []
            }
        },
        methods: {
            addBlockHandler: function(block) {
                let newBlock = JSON.parse(JSON.stringify(block));
                newBlock.index = this.blocks.length;
                this.blocks.push(newBlock);
            },
            openSettings(index) {
                this.activeSettings = this.blocks[index].options;
                this.activeBlock = index;
                this.settingsList = true;
            },
            updateOption(name, value) {
                // console.log(this.blocks[this.activeBlock], name, value);
                this.blocks[this.activeBlock].options[name] = value;
            },
            blockStyle(block) {
                let style = {};
                if (block.options.bgImage !== undefined) {
                    style.backgroundImage = "url(../img/" + block.options.bgImage + ")";
                }
                // console.log(style);
                return style;
            }
        },
        mounted() {
            // this.$on('addBlock', this.addBlockHandler)
        }
    };
</script>

<style scoped lang="scss">
    .fhh {
        width: 100%;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
        position: relative;
        text-align: center;

        background-size: cover;
        background-repeat: no-repeat;
        background-position: center center;
        background-attachment: fixed;
        background-color: #000;
        /*background-image: url(./assets/img1.jpg);*/

        &:after {
            content: '';
            display: block;
            width: 100%;
            position: absolute;
            top: 0;
            left: 0;
            height: 100vh;
            background-image: linear-gradient(to top, rgba(26,40,120,0.70), rgba(10,143,196,0.70));
        }

        .wrap {
            position: relative;
            z-index: 1;

        }
    }
    .col3 {
        .header-icon {
            margin: 20px;
            color: blue;
        }
        p {
            padding: 10px 20px;
        }
    }
</style>