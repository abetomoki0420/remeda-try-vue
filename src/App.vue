<script setup lang="ts">
import * as R from "remeda"
import { ref, computed } from "vue"

type Item = {
  name: string
  price: number
  grade: number
}

const item = ref<Item>({
  name: "カップラーメン",
  price: 200,
  grade: 1
})

const arr = ref([1, 10, 0, 12, 13, 3, 10])

const addProp = computed(() => {
  return R.addProp(item.value, "taste", "seafood")
})

const addPropDataLast = computed(() => {
  return R.addProp("taste", "curry")(item.value)
})

const allPass = computed(() => {
  return R.allPass(item.value, [
    (item: Item) => {
      return item.price < 100
    },
    (item: Item) => {
      return item.name === "カップラーメン"
    },
  ])
})

const anyPass = computed(() => {
  return R.anyPass(item.value, [
    (item: Item) => {
      return item.name === "カップラーメン"
    },
  ])
})

const chunk = computed(() => {
  return R.chunk(arr.value, 3)
})

const clamp = computed(() => {
  return R.clamp(item.value.price, {
    max: 100,
    min: 50,
  })
})

const clone = computed(() => {
  return R.clone(item.value)
})

const compact = computed(() => {
  return R.compact(arr.value)
})

const concat = computed(() => {
  return R.concat(arr.value, [20, 30, 40])
})

const countBy = computed(() => {
  return R.countBy(arr.value, (x: number) => {
    return x % 2 === 0
  })
})

const createPipe = computed(() => {
  return R.createPipe(
    (item: Item) => item.price * 2,
    (price) => price + 80
  )(item.value)
})

const difference = computed(() => {
  return R.difference(arr.value, [0, 12, 13])
})

const differenceWith = computed(() => {
  return R.differenceWith(
    [item.value, addProp.value, addPropDataLast.value],
    [item.value, addProp.value],
    R.equals
  )
})

const drop = computed(() => {
  return R.drop(arr.value, 2)
})

const dropLast = computed(() => {
  return R.dropLast(arr.value, 3)
})

const equals = computed(() => {
  return R.equals(item.value, {
    name: "カップラーメン",
    price: 200,
  })
})

const filteredArr = computed(() => {
  return R.filter(arr.value, (x) => x % 2 === 0)
})

const filteredIndexedArr = computed(() => {
  return R.filter.indexed(arr.value, (x, i) => i % 2 === 0)
})

const find = computed(() => {
  return R.find(arr.value, (x: number) => {
    return x % 2 === 0
  })
})

const findIndex = computed(() => {
  return R.findIndex(arr.value, (x: number) => {
    return x % 2 === 20
  })
})

const findLast = computed(() => {
  return R.findLast(arr.value, (x: number) => {
    return x % 2 === 0
  })
})

const findLastIndex = computed(() => {
  return R.findLastIndex(arr.value, (x: number) => {
    return x % 2 === 0
  })
})

const first = computed(() => {
  return R.first(arr.value)
})

const flatMap = computed(() => {
  return R.flatMap(arr.value, (x: number) => {
    return [x, x * 100]
  })
})

const flatMapToObj = computed(() => {
  return R.flatMapToObj(arr.value, (x: number) => {
    return x % 2 === 0 ? [[String(x), x * 100]] : []
  })
})

const flatten = computed(() => {
  return R.flatten([[arr.value], arr.value, [arr.value]])
})

const flattenDeep = computed(() => {
  return R.flattenDeep([[arr.value], arr.value, [arr.value]])
})

R.forEach(arr.value, (x) => {
  console.log({ x })
})

R.forEachObj(item.value, (x) => {
  console.log({ x })
})

const fromPairs = computed(() => {
  return R.fromPairs([
    [item.value.name, item.value.price],
    ["abc", 123],
  ])
})

const groupBy = computed(() => {
  return R.groupBy(arr.value, (x: number) => String(x).length)
})

const identity = computed(() => {
  return R.identity(item.value)
})

const indexBy = computed(() => {
  return R.indexBy(arr.value, (x: number) => x * 100)
})

const intersection = computed(() => {
  return R.intersection(arr.value, [10, 11, 12, 13])
})

const keys = computed(() => {
  return R.keys(item.value)
})

const last = computed(() => {
  return R.last(arr.value)
})

const map = computed(() => {
  return R.map(arr.value, (x: number) => x * 2)
})

const mapKeys = computed(() => {
  return R.mapKeys(item.value, (key) => `_${key}`)
})

const mapToObj = computed(() => {
  return R.mapToObj(arr.value, (x) => [x, x * 100])
})

const mapValues = computed( () => {
  return R.mapValues(item.value, (v) => R.isNumber(v) ? v * 100 : v )
})

const maxBy = computed( () => {
  return R.maxBy(arr.value, (x) => x)
})

const meanBy = computed( () => {
  return R.meanBy(arr.value, (x) => x)
})

const merge = computed( () => {
  return R.merge(item.value,{
    power: 100,
    pets: [1,2,3]
  })
})

const mergeAll = computed( () => {
  return R.mergeAll([item.value,{
    power: 100,
    pets: [1,2,3]
  }])
})

const minBy = computed( () => {
  return R.minBy(arr.value, (x) => x)
})

const noop = computed( () => {
  return R.noop()
})

const objOf = computed( () => {
  return R.objOf(100, 'key')
})

const omit = computed( () => {
  return R.omit(item.value, ['price'])
})

const omitBy = computed( () => {
  return R.omitBy(item.value, (value, key) => R.isNot(R.isString)(value))
})

const once = R.once( () => console.log("once"))
once()
once()

const partition = computed( () => {
  return R.partition(arr.value, (x) => x % 2 === 0)
})

const pathOr = computed( () => {
  return R.pathOr(item.value, ["price"], -1)
})

const pick = computed( () => {
  return R.pick( item.value, ["name"])
})

const pickBy = computed( () => {
  return R.pickBy( item.value, (value) => R.isString(value))
})

const pipe = computed( () => {
  return R.pipe(
    arr.value,
    R.map( x => x * 100),
    R.sumBy( x => x)
  )
})

const prop = computed( () => {
  return R.pipe(
    item.value,
    R.prop("name")
  )
})

// purry

const randomString = computed( () => {
  return R.randomString(5)
})

const range = computed( () => {
  return R.range(1,5)
})

const reduce = computed( () => {
  return R.reduce(arr.value, (acc, x) => acc + x + 1 , 0)
})

const reject = computed( () => {
  return R.reject( arr.value, (x) => x % 2 === 0)
})

const reverse = computed( () => {
  return R.reverse( arr.value )
})

const set = computed( () => {
  return R.set(item.value, "price" , 1000)
})

const sort = computed( () => {
  return R.sort( arr.value, (a,b) => a - b)
})

const sortBy = computed( () => {
  return R.sortBy([
    item.value,
    {
      name: "カレーラーメン",
      price: 300,
      grade: 1
    },
    {
      name: "トマトチーズラーメン",
      price: 350,
      grade: 2
    },
    {
      name: "トリュフラーメン",
      price: 800,
      grade: 3
    },
    {
      name: "塩ラーメン",
      price: 120,
      grade: 1
    },
  ],[
    (x) => x.grade, "desc"
  ],
  [(x) => x.price, 'desc'])
})

const splitAt = computed( () => {
  return R.splitAt(arr.value, 2)
})

const splitWhen = computed( () => {
  return R.splitWhen( arr.value, (x) => x > 10)
})

const sumBy = computed( () => {
  return R.sumBy(arr.value, (x) => x)
})

const take = computed( () => {
  return R.take(arr.value, 3)
})

const takeWhile = computed( () => {
  return R.takeWhile(arr.value, x => x < 13)
})

const times = computed( () => {
  return R.times(5, R.randomString)
})

const toPairs = computed( () => {
  return R.toPairs(item.value)
})

const type = computed( () => {
  return R.type(item.value.price)
})

const uniq = computed( () => {
  return R.uniq(arr.value)
})

const uniqBy = computed( () => {
  return R.uniqBy([
    item.value,
    {
      name: "カップラーメン",
      price: 200,
      grade: 2
    },{
      name: "カップラーメン",
      price: 300,
      grade: 1
    }
  ], (x) => x.grade)
})

const uniqWith = computed( () => {
  return R.uniqWith([
    item.value,
    {
      name: "カップラーメン",
      price: 200,
      grade: 2
    },{
      name: "カップラーメン",
      price: 300,
      grade: 1
    }
  ],R.equals)
})

const values = computed( () => {
  return R.values(item.value)
})

const zip = computed( () => {
  return R.zip(R.take(arr.value, 3), values.value)
})

const zipWith = computed( () => {
  return R.zipWith(R.take(arr.value, 3), values.value, (a, b) => `${a}:${b}`)
})


</script>

<template>
  <div>
    <p>item</p>
    {{ item }}
    <p>arr</p>
    {{ arr }}
  </div>
  <main>
    <div>
      <p>addProp</p>
      {{ addProp }}
    </div>
    <div>
      <p>addPropDataLast</p>
      {{ addPropDataLast }}
    </div>
    <div>
      <p>allPass</p>
      {{ allPass }}
    </div>
    <div>
      <p>anyPass</p>
      {{ anyPass }}
    </div>
    <div>
      <p>chunk</p>
      {{ chunk }}
    </div>
    <div>
      <p>clamp</p>
      {{ clamp }}
    </div>
    <div>
      <p>clone</p>
      {{ clone }}
    </div>
    <div>
      <p>compact</p>
      {{ compact }}
    </div>
    <div>
      <p>concat</p>
      {{ concat }}
    </div>
    <div>
      <p>countBy</p>
      {{ countBy }}
    </div>
    <div>
      <p>createPipe</p>
      {{ createPipe }}
    </div>
    <div>
      <p>difference</p>
      {{ difference }}
    </div>
    <div>
      <p>differenceWith</p>
      {{ differenceWith }}
    </div>
    <div>
      <p>drop</p>
      {{ drop }}
    </div>
    <div>
      <p>dropLast</p>
      {{ dropLast }}
    </div>
    <div>
      <p>equals</p>
      {{ equals }}
    </div>
    <div>
      <p>filteredArr</p>
      {{ filteredArr }}
    </div>
    <div>
      <p>filteredIndexedArr</p>
      {{ filteredIndexedArr }}
    </div>
    <div>
      <p>find</p>
      {{ find }}
    </div>
    <div>
      <p>findIndex</p>
      {{ findIndex }}
    </div>
    <div>
      <p>findLast</p>
      {{ findLast }}
    </div>
    <div>
      <p>findLastIndex</p>
      {{ findLastIndex }}
    </div>
    <div>
      <p>first</p>
      {{ first }}
    </div>
    <div>
      <p>flatMap</p>
      {{ flatMap }}
    </div>
    <div>
      <p>flatMapToObj</p>
      {{ flatMapToObj }}
    </div>
    <div>
      <p>flatten</p>
      {{ flatten }}
    </div>
    <div>
      <p>flattenDeep</p>
      {{ flattenDeep }}
    </div>
    <div>
      <p>fromPairs</p>
      {{ fromPairs }}
    </div>
    <div>
      <p>groupBy</p>
      {{ groupBy }}
    </div>
    <div>
      <p>identity</p>
      {{ identity }}
    </div>
    <div>
      <p>indexBy</p>
      {{ indexBy }}
    </div>
    <div>
      <p>intersection</p>
      {{ intersection }}
    </div>
    <div>
      <p>keys</p>
      {{ keys }}
    </div>
    <div>
      <p>last</p>
      {{ last }}
    </div>
    <div>
      <p>map</p>
      {{ map }}
    </div>
    <div>
      <p>mapKeys</p>
      {{ mapKeys }}
    </div>
    <div>
      <p>mapToObj</p>
      {{ mapToObj }}
    </div>
    <div>
      <p>mapValues</p>
      {{ mapValues }}
    </div>
    <div>
      <p>maxBy</p>
      {{ maxBy }}
    </div>
    <div>
      <p>meanBy</p>
      {{ meanBy }}
    </div>
    <div>
      <p>merge</p>
      {{ merge }}
    </div>
    <div>
      <p>mergeAll</p>
      {{ mergeAll }}
    </div>
    <div>
      <p>minBy</p>
      {{ minBy }}
    </div>
    <div>
      <p>noop</p>
      {{ noop }}
    </div>
    <div>
      <p>objOf</p>
      {{ objOf }}
    </div>
    <div>
      <p>omit</p>
      {{ omit }}
    </div>
    <div>
      <p>omitBy</p>
      {{ omitBy }}
    </div>
    <div>
      <p>partition</p>
      {{ partition }}
    </div>
    <div>
      <p>pathOr</p>
      {{ pathOr }}
    </div>
    <div>
      <p>pick</p>
      {{ pick }}
    </div>
    <div>
      <p>pickBy</p>
      {{ pickBy }}
    </div>
    <div>
      <p>pipe</p>
      {{ pipe }}
    </div>
    <div>
      <p>prop</p>
      {{ prop }}
    </div>
    <div>
      <p>randomString</p>
      {{ randomString }}
    </div>
    <div>
      <p>range</p>
      {{ range }}
    </div>
    <div>
      <p>reduce</p>
      {{ reduce }}
    </div>
    <div>
      <p>reject</p>
      {{ reject }}
    </div>
    <div>
      <p>reverse</p>
      {{ reverse }}
    </div>
    <div>
      <p>set</p>
      {{ set }}
    </div>
    <div>
      <p>sort</p>
      {{ sort }}
    </div>
    <div>
      <p>sortBy</p>
      {{ sortBy }}
    </div>
    <div>
      <p>pipe</p>
      {{ pipe }}
    </div>
    <div>
      <p>splitAt</p>
      {{ splitAt }}
    </div>
    <div>
      <p>splitWhen</p>
      {{ splitWhen }}
    </div>
    <div>
      <p>sumBy</p>
      {{ sumBy }}
    </div>
    <div>
      <p>take</p>
      {{ take }}
    </div>
    <div>
      <p>takeWhile</p>
      {{ takeWhile }}
    </div>
    <div>
      <p>times</p>
      {{ times }}
    </div>
    <div>
      <p>toPairs</p>
      {{ toPairs }}
    </div>
    <div>
      <p>type</p>
      {{ type }}
    </div>
    <div>
      <p>uniq</p>
      {{ uniq }}
    </div>
    <div>
      <p>uniqBy</p>
      {{ uniqBy }}
    </div>
    <div>
      <p>uniqWith</p>
      {{ uniqWith }}
    </div>
    <div>
      <p>values</p>
      {{ values }}
    </div>
    <div>
      <p>zip</p>
      {{ zip }}
    </div>
    <div>
      <p>zipWith</p>
      {{ zipWith }}
    </div>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-wrap: wrap;
  padding: 1rem;
}
main > div {
  width: 30%;
  flex-grow: 1;
}
main > div > p {
  font-weight: bold;
}
</style>
