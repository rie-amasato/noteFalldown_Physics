<template>
    <div
        class="canvas-physics"
        id="matter"
    />
</template>

<script setup> 
    import Matter from "matter-js"
    const Engine=Matter.Engine,
        Render=Matter.Render,
        Runner=Matter.Runner,
        Bodies=Matter.Bodies,
        Composite=Matter.Composite
        //World=Matter.World

    let engine

    const num_keys=ref(10)

    onMounted(()=>{
        const elm_matter=document.getElementById("matter")

        engine=Engine.create()
        const render=Render.create({
            element: elm_matter,
            engine,
            options: {
                width: elm_matter.offsetWidth,
                height: elm_matter.offsetHeight,
                background: "transparent",
                wireframeBackground: "transportent",
            }
        })

        Render.run(render)
        const runner=Runner.create()
        Runner.run(runner, engine)

        window.addEventListener("keydown", (e)=>{
            const int_key=parseInt(e.key)
            const x=elm_matter.offsetWidth/num_keys.value*int_key

            if (int_key) create_obj(x, 0, 20, 20)
        })
    })

    const create_obj=(x, y)=>{
        const obj=Bodies.circle(x, y, 40, 
            {
                render: {
                    strokeStyle: "transportent",
                    fillStyle: "#aa0",
                    opacity: 0.5,
                    lineWidth: 10,
                    sprite: {texture: "/IMG_1682.png"}
                },
            }
        )
        console.log(obj)

        Composite.add(engine.world, [obj])
    }
</script>

<style scoped>
.canvas-physics{
    background-color: #000000;
    width: 100vw;
    height: 100vh;
}
</style>