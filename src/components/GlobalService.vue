<template>
  <section id="global-service-examples">
    <div class="examples">
      <div class="parent">
        <label>Global Service example</label>
        <div class="wrapper">
          <div class="container" v-dragula="colOne" drake="first">
            <div v-for="text in colOne" :key="text" @click="onClick">{{text}} [click me]</div>
          </div>
          <div class="container" v-dragula="colTwo" drake="first">
            <div v-for="text in colTwo" :key="text">
              <span class="handle">+</span>
              <span>{{text}}</span>
            </div>
          </div>
        </div>
        <h4>Result</h4>
        <p>
          <h5>colOne</h5>
          <div v-for="text in colOne" :key="text">{{text}}</div>
        </p>

        <p>
          <h5>colTwo</h5>
          <div v-for="text in colTwo" :key="text">{{text}}</div>
        </p>
      </div>
    </div>

    <div class="examples" id="examples-2">
      <div class="parent">
        <label>Modify items in drake with transition</label>
        <div class="wrapper" v-for="container in categories">
          <div class="container" v-dragula="container" drake="second">
            <div v-for="number in container" :key="number" transition="scale">{{number}}</div>
          </div>
        </div>
        <button @click="testModify">Modify Items</button>
      </div>
    </div>

    <div class="examples" id="examples-3">
      <div class="parent">
        <label>Copy between containers</label>
        <div class="wrapper">
          <div class="container" v-dragula="copyOne" drake="third">
            <div v-for="text in copyOne" :key="text">{{text}}</div>
          </div>
          <div class="container" v-dragula="copyTwo" drake="third">
            <div v-for="text in copyTwo" :key="text">{{text}}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'globalService',

  data () {
    return {
      colOne: [
        'You can move these elements between these two containers',
        'Moving them anywhere else isn"t quite possible',
        'There"s also the possibility of moving elements around in the same container, changing their position'
      ],
      colTwo: [
        'This is the default use case. You only need to specify the containers you want to use',
        'More interactive use cases lie ahead',
        'Another message'
      ],
      categories: [
        [1, 2, 3],
        [4, 5, 6]
      ],
      copyOne: [
        'Lorem ipsum dolor sit amet, consectetuer adipiscing elit.',
        'Aenean commodo ligula eget dolor. Aenean massa.'
      ],
      copyTwo: [
        'Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.',
        'Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem.'
      ]
    }
  },
  created () {
    console.log('GLOBAL SERVICE: created')
    let service = this.$dragula.$service

    // IMPORTANT!! setup empty named drakes matching
    // directive drake configs in template
    // otherwise may (currently) result in conflict

    service.options('first', {
    })

    service.options('second', {
    })

    service.options('third', {
      copy: true
    })

    console.log('GLOBAL SERVICE: ready')
  },
  methods: {
    onClick () {
      window.alert('click event')
    },
    testModify () {
      this.categories = [
        ['a', 'b', 'c'],
        ['d', 'e', 'f']
      ]
    }
  }
}
</script>
