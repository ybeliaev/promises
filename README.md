# promises
```js

console.log("Начало тренировки..");

const TIME_ONE_PUSHUP = 200;
const TIME_ONE_SQUAT = 400;

const pushUp = (count) => {
  return new Promise((resolve, reject) => {
    if (count > 100) {
      reject(new Error("Приседаний нужно не более 100"));
    }
    setTimeout(() => {
      // вызов колбека в then:
      // также передача count с resolve позволит использовать это
      // значение в then в виде value
      resolve(count);
    }, count * TIME_ONE_PUSHUP);
  });
};
const squats = (count) => {
  return new Promise((resolve, reject) => {
    if (count > 50) {
      reject(new Error("Слишком много отжиманий. Нужно не более 50"));
    }
    setTimeout(() => {
      resolve(count);
    }, count * TIME_ONE_SQUAT);
  });
};

pushUp(5)
  .then((value) => {
    console.log(`Отжался ${value} раз`);
    return squats(10);
  })
  .then((value) => {
    console.log(`Присел ${value} раз`);
  })
  .catch((error) => {
    console.error("Что-то больше не могу...", error.toString());
  });
// *****************************
// ********async/await**********
// *****************************

const myTtraining = async () => {
  try {
    await pushUp(5);
    console.log("Отжался 5 раз");
    await squats(10);
    console.log("Присел 10 раз");
    return true;
  } catch (err) {
    console.error("Что-то больше не могу...", err);
    return false;
  }
};
myTtraining().then((result) => console.log(result));


```
