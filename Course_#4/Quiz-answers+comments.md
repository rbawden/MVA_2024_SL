# Quiz answers and comments

1. Is statistical MT relevant today?

- ❌ neural MT is always better.
- ❌ Yes, when dealing with a high-resource language pair.
- ✅ Yes, for certain tasks that do not require long-distance reordering.
  - *The example given in the class was one of normalisation of French texts from the 17th century into contemporary French, a type of translation task for which the word order of the input and output sequences are almost almost the same.*
- ❌ No, because they are too costly to train.

2. What is the main source of bias in MT models?

- ✅ The data on which they were trained.
   *- This is the main source of bias - a model will learn to reproduce (or exaggerate) statistical tendencies in the data.*
- ❌ The algorithms used to train them.
- ❌ Human evaluation.

3. Why might a smaller subword segmentation vocabulary be better for low-resource language pairs?

- ❌ There are fewer words to be covered, so it is not useful to have a bigger vocab.
   - *There are fewer words in the training data, but that does not mean that the language has fewer words that need to be covered.*
- ✅ There are fewer words to train on, so it is beneficial for generalisation and reducing the problem of unknown words.
  - *In general, when there is less data, it can be useful to choose a smaller subword vocabulary, which results in a higher degree of segmentation. There are fewer words in your training data, but you can hope that you have a better coverage (particularly of rare or unseen words) if you have more subwords.*
- ❌ There is not enough parallel data to train a good quality tokeniser.
  - *A tokeniser can be trained on monolingual data - it does not have to be parallel.* 

4. Which of these is a criticism of the BLEU metric?

- ❌ It is inversely correlated with human judgments of quality.
- ❌ It does not represent the overlap well between a reference translation and the output.
- ✅ It penalises good outputs that have different words from the reference translation.
   - *BLEU is based on exact n-gram matches and therefore cannot handle paraphrasing (or synonyms) well.*
- ✅ It is unable to handle synonyms.
   - *This is very similar to the above response. BLEU cannot handle synonyms.*

5. In statistical MT, we can model the probability of a translation t given a source sentence s as (P(s|t)P(t))/P(s) according to Bayes reformulation. When searching for the most probable translation, why can we remove the denominator (i.e. P(s))?

- ✅ The s is always the same regardless of the translation (it is a constant when applying argmax).
   - *For a given source sentence s, you do not need to calculate s when applying an argmax over possible translations because it is a constant.*
- ❌ The probabilities of the translation model already takes into account P(s).
- ❌ P(s) only varies very slightly and therefore removing it is fine to make a good approximation when applying an argmax.
- ❌ P(s) is always the same, whatever the source sentence s, given that it is a well-formed sentence.

6. A multilingual model that has separate encoders and decoders for each language...

- ❌ Is equivalent to having separate encoder-decoder models for each language pair.
  - *The difference is that in the multilingual variant, models are encouraged to represent the different languages in the same internal representation space. This is facilitated by having language pairs that have the same source or target languages (e.g. en-fr, en-de, en-cs and de-fr, cs-fr, zh-fr). Having an encoder-decoder per language pair makes each model separate and nothing encourages the internal representations to be in the same space for different models.*
- ❌ Enables vocabulary sharing across languages.
  - *If each language has its own encoder and decoder, the vocabulary is not shared. A universal MT model such as the one by Google (Johnson et al.) has a single encoder and decoder shared for all languages and this one does encourage vocab sharing.*
- ✅ Encourages languages to be encoded in a shared representation space.
  - *The idea here is that you encourage languages to be encoded into a multilingual embedding space and each decoder can be trained to decode from that space. This is the case even if each language has its own encoder into the space and its own decoder out of the space.*
- ✅ Could theoretically work for zero-shot language directions (i.e. for language directions that it was not explicitly trained on).
  - *If trained well, you could potentially translation between a new language direction, provided that the source and target language have been seen in the training data as part of other language directions.*

7. Why is forward translation less popular than backtranslation?

- ❌ Backtranslation enables you to back-propagate through the network and learn better.
- ✅ It helps the model to produce good quality target-language outputs.
   -  *Backtranslation involves taking origin target-language texts and produce an artificial translation of the source-side. Training on such data means that the model is learning on noisy source sentences (not so bad) and good target sentence. Forward translations are the opposite, and while it can still be beneficial, there is a risk that the model learn to produce noisy outputs, because that is what is was trained one.*
- ❌ We always have less data in that direction.

8. What are the advantages of a cross-attention mechanism in an encoder-decoder model?

- ✅ It enables the decoder to focus on specific source tokens.
   - *Different source tokens may be important at each decoder step and attention enables us to create a representation with variable contributions from source tokens.*
- ✅ It helps the model to represent a variable length sequence in a fixed size representation.
   - *This is also true. In an RNN model without attention, a variable length sequence is being represented by a fixed size representation (same for all decode steps). Performance suffers for longer sequences because more information is going into the same vector, which is not specialised for each decoder step. Using an attention mechanism helps this problem of representing a variable-length sequence with a fixed-size vector, because the content can be adapted to each step.*
- ❌ It helps the decoder to produce more fluent translations.
- ❌ It gives all source tokens access to their left and right context

N.B. The second correct answer to this question was more indirect and therefore harder to get. With only 3 complete correct answers to this question, I will be giving 1/5 point for one of the two correct answers.
 
