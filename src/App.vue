<script setup>
import { ref, onMounted } from 'vue'

import Poses from './components/pose_test.vue'

const faces = ['face_up', 'face_down', 'right', 'left', 'vertical_up', 'vertical_down']

let instrument_settings = (i) => {
  let n = 1
  let calc = x => n > 0 ? x - 1 : x

  let [f, s, v] = [
    calc(i.poses.faces), 
    calc(i.poses.sides), 
    calc(i.poses.vertical)
  ]
  
  let face_option = f > 2 ? [faces[1]] 
  : f > 1 ? [faces[0]] 
  : f > 0 ? [faces[0], faces[1]] 
  : []
  let sides = s > 2 ? [faces[2]] 
  : s > 1 ? [faces[3]] 
  : s > 0 ? [faces[3], faces[2]] 
  : []
  let vertical = v > 2 ? [faces[5]]
  : v > 1 ? [faces[4]] 
  : v > 0 ? [faces[4], faces[5]] 
  : []

  return [...face_option, ...sides, ...vertical]
}

const cubes = ref([])
const hl = ref([])

const chng_face = (i, face) => {
  let c = cubes.value.filter(ii => ii[0] != i)
  let h = hl.value.filter(ii => ii[0] != i)
  c.push([i, `show-${face}`])
  h.push([i, face])
  cubes.value = c
  hl.value = h
}

const getCube = i => {
  let c = cubes.value.filter(ii => ii[0] == i)
  return c.length > 0 ? c[0][1] : null
}

const getHL = (i, face) => {
  let h = hl.value.filter(ii => ii[0] == i)
  return h.length > 0 && h[0][1] == face ? true : false
}
</script>

<template>

  <div style="margin: 10px;">
    Tech test - Tasks:

    <div>

      <b class="task">A. Vue</b>
      <ol>
        <li>display all values given in the 'properties' object for each entry, use your judgment on how to display them</li>
        <li>find the inconsistency between the values and fields in `proto_demo`</li>
        <li>convert the pose buttons to a dropdown menu using the vue composition api bindings to set the face of the cube (space-out contents of each entry as you see fit)</li>
        <li>change the background color of each blue container on hover by using the vue action and binding the hover sass class</li>
      </ol>
      <b class="task">B. Store</b>
      <ol>
        <li>create a pinia store</li>
        <li>move current functions to manage the state of the cubes, faces and the highlighted face to the store</li>
        <li>load values into the store on mount of `App` component</li>
      </ol>
      <b class="task">C. Project</b>
      <ol>
        <li>Push to a new branch `deps {yymmdd}`</li>
        <li>resolve the 4+ 'High' impact vulnerabilities</li>
        <li>Commit with message listing solutions</li>
        <li>PR to main adding me 'SirJamesBrown' as reviewer</li>
      </ol>
      <b class="task">D. Execution</b>
      <ol>
        <li>build and serve with the provided scripts in package.json</li>
        <li>using the express server `./server.js`, create a POST end-point which takes a string and call it from the vue app with any given arg</li>
        <li>Linux | Mac: use node `exec` (specifically) to create a new file called 'word' containing the passed arg and the timestamp (Unix format)</li>
        <li>Windows: use an fs tool to create a new file called 'word' with the passed arg</li>
        <li>create a GET endpoint on the server to read the file and return the contents to the vue app</li>
        <li>display the file contents in the app</li>
        <li>as in section 'C', commit and pr</li>
      </ol>

    </div>

    <div>
      Strike though completed tasks.<br />
      Not all tasks need to be completed. Please highlight those skipped or passed with a note.
    </div>

  </div>

  <Poses :faces
  :chng_face :getCube :getHL :instrument_settings />

</template>

<style scoped lang="sass">
.task
  margin: 10px
  font-size: 12px
  font-weight: bold
</style>
