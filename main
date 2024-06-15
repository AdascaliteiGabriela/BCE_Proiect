breed [inns inn]
breed [workers worker]
breed [ buildings building ]

workers-own
[
  hunger
  energy
]
to setup
  clear-all
  setup-inns
  setup-workers
  setup-patches
  reset-ticks
end

to setup-workers
  set-default-shape turtles "person construction"
  create-workers number-agents
  ask workers
  [
    setxy random-pxcor random-pycor
    set energy 100
    set hunger 0
  ]
end

to setup-inns
  clear-all
  create-inns 1
  ask inns
  [
    set shape "inn"
    set size 4
    move-to patch -14 -7
  ]
end

to setup-patches
  ask patches
  [
    set pcolor green
    if pycor < 5 and pycor > -5 [ set pcolor brown ]
    if (((pycor = 7 or pycor = -7) and pxcor mod 5 = 1))[ set pcolor grey ]
    ask patch -14 -7 [set pcolor green]
  ]
end

to build-road
  ask workers
  [
    right random 360
    left random 360
    fd 1
    set energy energy - 2
    if pycor = 0 and pxcor mod 2 = 1
    [
      set pcolor white
      set energy energy - (5 + random 11)
    ]
    if pcolor = brown
    [
      set pcolor black
      set energy energy - (5 + random 11)
    ]
     if energy <= 25
    [
      set hunger 1
      move-to patch -14 -7
      eat-workers
    ]
    ifelse show-energy? [ set label energy ]
      [set label ""]
  ]
end

to create-houses
  ask patches with [pcolor = gray]
  [
    if any? workers-here
    [
      sprout 1 [ set shape "building" set size 3]
      ask buildings [
  ]

      set pcolor green
      ask workers-here [
        set energy (energy - 25)
      ]
    ]
  ]
end

to eat-workers
  ask workers [
    if hunger > 1
    [
      set hunger hunger - 1
      move-to patch -14 -7
    ]
   if hunger = 1
    [
      set energy 100
      move-to one-of patches with [ pycor > -10 and pycor < 10 ]
    ]
    ]
end

to go
  build-road
  create-houses
  if count patches with [pcolor = brown or pcolor = gray] = 0 [stop]
  let avg-energy mean [energy] of workers
  plot avg-energy
  tick
end
