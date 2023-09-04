```
// computed带类型
const nameAndCountry: ComputedRef<string> = computed((): string => `
const props = defineProps({
modelValue: {
      type: Object,
      required: true
    },
})

const emit = defineEmits(['update:modelValue'])

const formData = ref({ ...props.modelValue })
watch(
      formData,
      (newValue) => {
        console.log(newValue)
        emit('update:modelValue', newValue)
      },
      {
        deep: true, //如果后续 v-model 绑定的是 formData的属性值(而不是 formData本身),则需要开启深度监听,否则后续 v-model 修改无法触发监听更新
      }
    )
```

```
v-model 用法

const props = defineProps({
modelValue: {
      type: Object,
      required: true
    },
})

const emit = defineEmits(['update:modelValue'])

const formData = ref({ ...props.modelValue })
watch(
      formData,
      (newValue) => {
        console.log(newValue)
        emit('update:modelValue', newValue)
      },
      {
        deep: true, //如果后续 v-model 绑定的是 formData的属性值(而不是 formData本身),则需要开启深度监听,否则后续 v-model 修改无法触发监听更新
      }
    )
```

```
// computed带类型
const nameAndCountry: ComputedRef<string> = computed((): string => `The movie name is ${movieName.value} from ${country.value}`);

// getter setter
const nameAndCountry: WritableComputedRef<string> = computed({
  get(): string {
    return 'somestring'
  },
  set(newValue: string) {
    // set something
  },
});
```

```
// store/index.ts
import { createStore, Store, useStore as useVuexStore } from 'vuex'

import login from './login/login'
import system from './main/system/system'

import { IRootState, IStoreType } from './types'

const store = createStore<IRootState>({
  state() {
    return {
      name: 'coderwhy',
      age: 18
    }
  },
  mutations: {},
  getters: {},
  actions: {},
  modules: {
    login,
    system
  }
})

export function setupStore() {
  store.dispatch('login/loadLocalLogin')
}

export function useStore(): Store<IStoreType> {
  return useVuexStore()
}

export default store

//store/types.ts

import { ILoginState } from './login/types'
import { ISystemState } from './main/system/types'

export interface IRootState {
  name: string
  age: number
}

export interface IRootWithModule {
  login: ILoginState
  system: ISystemState
}

export type IStoreType = IRootState & IRootWithModule


```

```
//plugin
export default {
  install(app) {
    app.config.globalProperties.$name = "coderwhy"
  }
}

//main.js
import pluginObject from './plugins/plugin.js'
app.use(pluginObject);

// composition api 方法使用
import { getCurrentInstance } from "vue";
const instance = getCurrentInstance();
console.log(instance.appContext.config.globalProperties.$name);


```
