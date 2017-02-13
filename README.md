# NBC Take Home Tasks


##### Task No. 1:
### Convert a string to piglatin.

- Vowels – add 'yay' to the end.
- Consonants – all letters before first vowel are appended to the end of the word and 'ay' is then added to the end of the word.
- Words that were capitialized should remained capitialized at the beginning of the word.

e.g. `convertToPigLatin("This is a great place to work.")` would be `"Isthay isyay ayay eatgray aceplay otay orkway"`

##### Solution for Task No. 1:

```
const str = 'This is a Great Place to Work';

const convertToPigLatin = str => {
    return str.
        split(' ').
        map(word => {
            let arr = word.split('');
            const first = arr[0];
            const test = {
                isUppercase (letter) {
                    return /[A-Z]/.test(letter);
                },
                isVowel (letter) {
                    return /[aeiou]/.test(letter);
                },
                willCapitalize (word, first) {
                    const capitalize = word => `${word.charAt(0).toUpperCase()}${word.slice(1).toLowerCase()}`;
                    return this.isUppercase(first) ? capitalize(word) : word;
                }
            };

            if (test.isVowel(first)) {
                let finalWord = `${word}yay`;
                return test.willCapitalize(finalWord, first);
            }
            while (!test.isVowel(arr[0])) {
                const toEnd = arr.shift();
                arr.push(toEnd);
            }
            
            let finalWord = `${arr.join('')}ay`;
            
            return test.willCapitalize(finalWord, first);
        });
}; 
```

##### Task No. 2:
### Summarize a multidimensional array.

e.g. `ex: summarizeArr([1,2,3,[4,5]])` should equal `15`.

##### Solution for Task No. 2:

```
const arr = [[[1,2,3,4,5],[[1],[2],[3],[4],[5],[6],[[1]]],[9,8,7,6,5,[1,2,3]]],[10,20,30,40,50],[21,33,55,66,77,88],[11,12,13,14,15,16,17,18,19],[[1000,1234],154,2122],[45,66,88,99,100,101]];

const summarizeArr = arr => {
  let sum = 0;
  arr.forEach(v => sum += (typeof v === 'object') ? summarizeArr(v) : v);
  return sum;
};
```


##### Task No. 3:
### Find value based on id.

e.g. `getValue(12).value` should equal `A-B-C`.

##### Solution for Task No. 3:

```
const data = [
  {
    id: 1,
    value: 'A',
    children: [
      {
        id: 3,
        value: 'A-A',
        children: [{id: 7,value: 'A-A-A'}, {id: 8,value: 'A-A-B'}, {id: 9,value: 'A-A-C'}]
      },
      {
        id: 4,
        value: 'A-B',
        children: [{id: 10,value: 'A-B-A'}, {id: 11,value: 'A-B-B'}, {id: 12,value: 'A-B-C'}]
      }
    ]
  },
  {
    id: 2,
    value: 'B',
    children: [
      {
        id: 5,
        value: 'B-A',
        children: [{id: 13,value: 'B-A-A'}, {id: 14,value: 'B-A-B'}, {id: 15,value: 'B-A-C'}]
      },
      {
        id: 6,
        value: 'B-B',
        children: [{id: 16,value: 'B-B-A'}, {id: 17,value: 'B-B-B'}, {id: 18,value: 'B-B-C'}]
      }
    ]
  }
];

const getValue = (id, arr = data) => {
  let childArr = [];

  for (let i = 0; i < arr.length; i++) {
    const obj = arr[i];
    if (obj.id === id) return obj.value;
    if (obj.children) {
      const { children } = obj;
      childArr = [...childArr, ...children];
    }
  }
  
  return childArr.length ? getValue(id, childArr) : `{ id: ${id} } was not found!`;
}
```
