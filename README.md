# BoardEye
Line of sight detector using deep learning technology

## Motivation
Just wanted to use Keras and Vision API :)

## What does it do?
- Capture your face by a webcam (tested only on Mac), and classify it by Google Vision API
- Train a neural network based on results from Vision API
- Predict input from a webcam

At the end, your neural network should be able to classify whether you are looking at the display or now.

## Setup
Assuming that you already have NodeJS and Keras working.

```sh
npm install
export GOOGLE_API_KEY=XXXXXX
```

If you would like to try prediction now, download a trained [model](https://drive.google.com/open?id=0B9nFZuxm88eRb1F4ZUtJQTZKcDQ) and place them under `data`. Then go `Prediction` section below.

## Generating Training Data
You need two kinds of pictures - looking at your display or not.

So, to collect **looking**(=1) data, run
```sh
node capture.js -d data/1
```

To collect **not looking**(=0) data, also run
```sh
node capture.js -d data/0
```

Repeat above as many times as you can. More data, always better. So, I've done like
```sh
for i in {1..10}; do
  echo progress $i
  say "$i"
  ./capture.js -d data/1
done
```

Then let's convert them to CSV files
```sh
node csvgen.js -d data/1 > data/csv/1.csv
node csvgen.js -d data/0 > data/csv/0.csv
```

## Training
After generating a bunch of data, it's time to train a brain
```sh
python train.py
```

It defaults to 5000 epoch. Generated model and weights are automatically saved. If you would like to train more, just run it again.

## Prediction
All set. Let's test it out!
```sh
node capture.js
```

Then copy the output, then
```sh
python predict.py COPIED_TEXT
```

Now you should see 0 or 1. Did it work? :)
