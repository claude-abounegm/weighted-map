# weighted-map

A simple ascending weighted map

```js
const WeightedMap = require('weighted-map');

const MAX_WEIGHT = 4;

// will initialize a map with a maximum individual
// weight of 4. Each entry in the map cannot exceed
// weight 4
const map = new WeightedMap(MAX_WEIGHT);

map.add('A', 'My key is A');
map.add('B', 'My key is B');
map.add('C', 'My key is C');
map.add('D', 'My key is D');
```

## Round Robin
```js
// Round robin with max weight
let item;
while ((item = map.next())) {
    console.log(item.key);
}

// the above will loop through all
// items in the map and will increase
// the weight of every item by 1
// until the weight of every item
// becomes 4. the loop then stops.
```

The above is an example and there are several uses for this.

## Definitions
```ts
interface WeightedKeyValuePair<K, V> {
    weight: number;
    readonly key: K;
    readonly value: V;
}

class WeightedMap<K, V> {
    constructor(maxWeight?: number);

    readonly first: WeightedKeyValuePair<K, V> | undefined;
    readonly size: number;

    clear(): WeightedMap<K, V>;

    has(key: K): boolean;
    get(key: K): WeightedKeyValuePair<K, V>;

    add(key: K, value: V, initialWeight?: number): WeightedKeyValuePair<K, V>;
    update(key: K, value: V): WeightedKeyValuePair<K, V>;
    delete(key: K): WeightedKeyValuePair<K, V> | undefined;

    next(weightIncrement?: number): WeightedKeyValuePair<K, V> | undefined;

    entries(): IterableIterator<WeightedKeyValuePair<K, V>>;
    entries<T>(transform: (entry: WeightedKeyValuePair<K, V>) => T): IterableIterator<T>;

    entriesArray(): WeightedKeyValuePair<K, V>[];
    entriesArray<T>(transform: (entry: WeightedKeyValuePair<K, V>) => T): T[];
}
```