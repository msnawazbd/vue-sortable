<template>
    <div class="hello">

        <draggable @end="onEnd" ghost-class="ghost" v-model="myArray">
            <transition-group name="flip-list" type="transition">
                <div :id="element.id" :key="element.id" class="sortable" v-for="element in myArray">
                    <strong>{{ element.name }}</strong>
                    <span>{{ element.id }}</span>
                </div>
            </transition-group>
        </draggable>

        <p><strong>Previous Index: </strong> {{ oldIndex }}</p>
        <p><strong>New Index: </strong> {{ newIndex }}</p>

    </div>
</template>

<script>

    import draggable from 'vuedraggable'

    export default {
        name: 'HelloWorld',
        components: {
            draggable
        },
        props: {
            msg: String
        },
        data(){
            return {
                myArray: [
                    { name: "Angular", id: 0 },
                    { name: "React", id: 1 },
                    { name: "Vue", id: 2 },
                    { name: "HTML", id: 3 },
                    { name: "CSS", id: 4 },
                    { name: "Sass", id: 5 }
                ],
                oldIndex: '',
                newIndex: ''
            }
        },
        methods: {
            onEnd: function (evt) {
                this.oldIndex = evt.oldIndex;
                this.newIndex = evt.newIndex;
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
    h3 {
        margin: 40px 0 0;
    }

    strong {
        display: inline-block;
    }

    .sortable {
        width: 100%;
        background: white;
        padding: 1em;
        cursor: move;
        margin-bottom: 2px;

        span {
            float: right;
        }
    }

    .hello .sortable-drag{
        opacity: 0;
    }

    .flip-list-move {
        transition: transform 0.5s;
    }

    .ghost{
        border-left: 6px solid rgb(0, 183, 255);
        box-shadow: 10px 10px 5px -1px rgba(0,0,0,0.14);
        opacity: .7;

        &::before {
            content: " ";
            position: absolute;
            width: 30px;
            height: 30px;
            margin-left: -50px;
            background-image: url('../assets/drag.png');
        }
    }
</style>
