# machine-learning-text
An attempt to write an artificial intelligence that generates text

import numpy as np

text = open('Text.txt', encoding='utf-8').read()

separate = text.split()


def make_pairs(separate):
    for i in range(len(separate) - 1):
        yield (separate[i], separate[i + 1])


pairs = make_pairs(separate)

word_dict = {}

for word_1, word_2 in pairs:
    if word_1 in word_dict.keys():
        word_dict[word_1].append(word_2)
    else:
        word_dict[word_1] = [word_2]


first_word = np.random.choice(separate)

while first_word.islower():
    first_word = np.random.choice(separate)

chain = [first_word]

n_words = 100

for i in range(n_words):
    randomm = np.random.choice(word_dict[chain[-1]])
    if randomm == word_dict[chain[-1]]:
        randomm = word_dict[chain[-2]]
    chain.append(randomm)


print(' '.join(chain))
