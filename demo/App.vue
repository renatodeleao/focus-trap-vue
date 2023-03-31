<template>
  <div>
    <h1 tabindex="0">focus-trap demo</h1>

    <p>
      <span style="font-size: 2em; vertical-align: middle">☜</span>
      <a
        href="https://github.com/posva/focus-trap-vue"
        style="vertical-align: middle"
        >Return to the repository</a
      >
    </p>

    <p>
      In the demos below, you'll be able to tell that a focus trap is active
      because it will turn pink. You should also be able to tell because it will
      trap your focus!
    </p>

    <p>
      When a trap is active, you can deactivate it by pushing its deactivate
      button or, if the demo allows, hitting
      <kbd>Escape</kbd>.
    </p>

    <section id="basic">
      <h2>default behavior</h2>
      <p>
        <button id="activate-default" @click="demos.basic.isActive = true">
          activate trap
        </button>
      </p>

      <focus-trap v-model:active="demos.basic.isActive">
        <div
          class="trap"
          :class="demos.basic.isActive && 'is-active'"
          tabindex="-1"
        >
          <p>
            Here is a focus trap
            <a href="#">with</a>
            <a href="#">some</a>
            <a href="#">focusable</a> parts.
          </p>
          <p>
            <button
              id="deactivate-default"
              @click="demos.basic.isActive = false"
            >
              deactivate trap
            </button>
          </p>
        </div>
      </focus-trap>
    </section>

    <section id="vif">
      <h2>With v-if (ie: transitioning component)</h2>
      <p>
        <button id="activate-default" @click="demos.vif.isActive = true">
          activate trap
        </button>
      </p>
      <focus-trap v-model:active="demos.vif.isActive">
        <transition name="fade" appear>
          <div
            class="trap"
            v-if="demos.vif.isActive"
            :class="demos.vif.isActive && 'is-active'"
            tabindex="-1"
            ref="vifContainer"
          >
            <p>
              Here is a focus trap
              <a href="#">with</a>
              <a href="#">some</a>
              <a href="#">focusable</a> parts.
            </p>
            <p>
              <button
                id="deactivate-default"
                @click="demos.vif.isActive = false"
              >
                deactivate trap
              </button>
            </p>
          </div>
        </transition>
      </focus-trap>
    </section>

    <section id="iene">
      <h2 id="iene-heading">initial element, no escape</h2>
      <p>
        When this focus trap activates, focus jumps to a specific, manually
        specified element.
      </p>
      <p>
        Also, in this demo the
        <kbd>Escape</kbd> key does not deactivate the focus trap. You must click
        the button.
      </p>
      <p>
        <button @click="demos.iene.isActive = true">activate trap</button>
      </p>

      <focus-trap
        v-model:active="demos.iene.isActive"
        :initial-focus="demos.iene.initialFocus"
        :escape-deactivates="false"
      >
        <div class="trap" :class="demos.iene.isActive && 'is-active'">
          <p>
            Here is a focus trap
            <a href="#">with</a>
            <a href="#">some</a>
            <a href="#">focusable</a> parts.
          </p>
          <p>
            <label class="inline-label">
              Initially focused input
              <input ref="ieneInput" />
            </label>
          </p>
          <p>
            <button @click="demos.iene.isActive = false">
              deactivate trap
            </button>
          </p>
        </div>
      </focus-trap>
    </section>
    <section id="ocd">
      <h2 id="ocd-heading">Click outside deactivates</h2>
      <p>
        When this focus trap activates, focus jumps to a specific, manually
        specified element.
      </p>
      <p>
        Also, in this demo the
        <kbd>Escape</kbd> key does not deactivate the focus trap. You must click
        the button.
      </p>
      <p>
        <button @click="demos.ocd.isActive = true">activate trap</button>
      </p>

      <focus-trap
        v-model:active="demos.ocd.isActive"
        :click-outside-deactivates="true"
      >
        <div class="trap" :class="demos.ocd.isActive && 'is-active'">
          <p>
            Here is a focus trap
            <a href="#">with</a>
            <a href="#">some</a>
            <a href="#">focusable</a> parts.
          </p>
          <p>
            <label class="inline-label">
              Initially focused input
              <input ref="ieneInput" />
            </label>
          </p>
          <p>
            <button @click="demos.ocd.isActive = false">deactivate trap</button>
          </p>
        </div>
      </focus-trap>
    </section>

    <section id="aoc">
      <h2 id="aoc-heading">allow outside click</h2>
      <p>
        A callback function can be used to determine whether or not you should
        be allowed to click outside of the focus trap when it's deactivated.
      </p>
      <p>
        <label>
          <input type="checkbox" v-model="demos.aoc.clickOutsideEnabled" />
          Enable outside clicking
        </label>
      </p>
      <p>
        <button @click="demos.aoc.isActive = true">activate trap</button>
      </p>

      <focus-trap
        v-model:active="demos.aoc.isActive"
        :allow-outside-click="demos.aoc.allowOutsideClick"
      >
        <div class="trap" :class="demos.aoc.isActive && 'is-active'">
          <p>
            Here is a focus trap <a href="#">with</a> <a href="#">some</a>
            <a href="#">focusable</a> parts.
          </p>
          <p>
            <label class="inline-label">
              Some input
              <input ref="ocdInput" />
            </label>
          </p>
          <p>
            <button @click="demos.aoc.isActive = false">deactivate trap</button>
          </p>
        </div>
      </focus-trap>
      <p>
        <button id="aoc-outside-button" @click="handleClickFromAOC">
          Try clicking me after activating the focus trap!
        </button>
      </p>
    </section>

    <section id="methods">
      <h2 id="methods-heading">exposed methods</h2>
      <p>
        Uses the methods exposed by the component (via $refs attachment) to
        activate and deactivate the focus trap
      </p>
      <p>
        <button @click="() => $refs.methodsFocusTrap.activate()">
          activate trap
        </button>
      </p>

      <focus-trap
        ref="methodsFocusTrap"
        v-model:active="demos.methods.isActive"
      >
        <div class="trap" :class="demos.methods.isActive && 'is-active'">
          <p>
            Here is a focus trap
            <a href="#">with</a>
            <a href="#">some</a>
            <a href="#">focusable</a> parts.
          </p>
          <p>
            <label class="inline-label">
              Some input
              <input ref="ieneInput" />
            </label>
          </p>
          <p>
            <button @click="() => $refs.methodsFocusTrap.deactivate()">
              deactivate trap via method call
            </button>
          </p>
        </div>
      </focus-trap>
    </section>

    <section id="vue-components">
      <h2>Wrapping Vue Components</h2>

      <p>
        <button @click="demos.comp.isActive = true">activate trap</button>
      </p>

      <focus-trap v-model:active="demos.comp.isActive">
        <SampleComponent
          class="trap"
          :class="demos.comp.isActive && 'is-active'"
          tabindex="-1"
        >
          <p>
            <button @click="demos.comp.isActive = false">
              deactivate trap
            </button>
          </p>
        </SampleComponent>
      </focus-trap>
    </section>

    <!--
      Based on https://github.com/focus-trap/focus-trap/blob/da97007787235571a394544ed85ec31445f2069e/docs/index.html#L292
    -->
    <section id="nested">
      <h2 id="nested-heading">nested</h2>
      <p>
        Nested focus traps.
        <blockquote>
          So I have nested Traps, both with the prop <code>clickOutsideDeactivates</code>. However when I click outside both traps while the inner one is active only the inner one closes.
          Is there a pattern I can use to close both traps if the click is outside of both, or just the inner trap if the click is outside the inner trap but within the outer one?
          https://github.com/focus-trap/focus-trap-react/discussions/942
        </blockquote>
      </p>
      <p>
        <button id="nested-activate-outer" aria-describedby="nested-heading" @click="demos.nested.outer.isActive = true">
          activate outer trap
        </button>
        <button id="nested-activate-outer" aria-describedby="nested-heading" @click="demos.nested.clickOutsideDeactivatesBoth = true">
          Click outside deactivates both: {{ demos.nested.clickOutsideDeactivatesBoth }}
        </button>
      </p>
      <focus-trap
        v-model:active="demos.nested.outer.isActive"
        :click-outside-deactivates="demos.nested.outer.onClickOutsideDeactivates"
        @pause="demos.nested.outer.onPauseCalledTimes++"
        @post-pause="demos.nested.outer.onPostPauseCalledTimes++"
        @unpause="demos.nested.outer.onUnpauseCalledTimes++"
        @post-unpause="demos.nested.outer.onPostUnpauseCalledTimes++"
      >
        <div id="nested-outer" class="trap" :class="demos.nested.outer.isActive && 'is-active'" tabindex="-1">
          <p>
            <button id="nested-deactivate-outer" aria-describedby="nested-heading" @click="demos.nested.outer.isActive = false">
              deactivate outer trap
            </button>
          </p>
          <p>
            <button id="nested-activate-inner" aria-describedby="nested-heading" @click="demos.nested.inner.isActive = true">
              activate inner trap
            </button>
          </p>
          <p>
            <button >
              NOTHING
            </button>
          </p>
          <focus-trap
            v-model:active="demos.nested.inner.isActive"
            :click-outside-deactivates="demos.nested.inner.onClickOutsideDeactivates"
          >
            <div id="nested-inner" class="trap" :class="demos.nested.inner.isActive && 'is-active'" style="padding:5px 10px;">
              <p>
                <button>
                  nothing
                </button>
              </p>
              <p>
                <button id="nested-deactivate-inner" aria-describedby="nested-heading" @click="demos.nested.inner.isActive = false">
                  deactivate and close inner trap
                </button>
              </p>
            </div>
          </focus-trap>
        </div>
      </focus-trap>
      <pre>{{ demos.nested }}</pre>
    </section>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
import { FocusTrap } from '../src'
import SampleComponent from './components/SampleComponent.vue'

const ieneInput = ref<HTMLInputElement>()

const demos = reactive({
  basic: {
    isActive: false,
  },
  vif: {
    isActive: false,
  },
  iene: {
    initialFocus: () => ieneInput.value,
    isActive: false,
  },
  ocd: {
    isActive: false,
  },
  aoc: {
    isActive: false,
    clickOutsideEnabled: false,
    allowOutsideClick: () => demos.aoc.clickOutsideEnabled,
  },
  methods: {
    isActive: false,
  },
  comp: {
    isActive: false,
  },
  nested: {
    clickOutsideDeactivatesBoth: false,
    outer: {
      onClickOutsideDeactivates: () => true,
      isActive: false,
      onPauseCalledTimes: 0,
      onPostPauseCalledTimes: 0,
      onUnpauseCalledTimes: 0,
      onPostUnpauseCalledTimes: 0
    },
    inner: {
      onClickOutsideDeactivates: (e) => {
        // console.log(e.target)
        // console.log(e.target.closest('#nested-outer'))
        // if(!e.target.closest('#nested-outer') && demos.nested.clickOutsideDeactivatesBoth) {
        //   console.log('yoo')
        //   demos.nested.outer.isActive = false
        // }
        return true
      },
      isActive: false
    },
  }
})
</script>

<style>
body {
  color: #333;
  font-family: 'Helvetica Neue', 'Helvetica', Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 1.4;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  max-width: 600px;
  margin: 0 auto 200px;
  padding: 10px;
}

*:focus {
  outline: 5px solid lightblue;
}

.trap {
  border: 1px solid #ccc;
  padding: 1em 2em;
}

.trap.is-active {
  background: #fee9ff;
}

.trap.is-active .trap.is-active {
  background: rgba(0,0,0,0.1)
}

.inline-label {
  margin-right: 0.5em;
}

#demo-four,
#initial-nine {
  outline: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.fade-leave-from,
.fade-enter-to {
  opacity: 1;
}

code,
kbd {
  background: #eee;
  font-size: 90%;
  padding: 0 2px;
}

blockquote {
  border-left: 2px solid;
  padding-left: 10px;
  margin-left: 0px;
  font-style: italic;
}
</style>
