
![](img/4e7230a4ecf676d308ca85f3d2e65bae_38_0.png)

Figure 1.11 Early network-like models. Left: Barends’s (1971) model (redrawn); R is a receptor in the receptive field of unit E, which evaluates the input received; S sums signals from the E units. Middle: Thompson’s (1965) suggestion of neural circuitry underlying generalization, whereby physically distinct stimuli (A and B) may activate overlapping sets of neurons, thus eliciting similar behavior (smaller circles are inhibitory neurons). Reprinted by permission from Mostofsky, ed., Stimulus Generalization. © 1965 by the Board of Trustees of the Leland Stanford Jr. University. Right: Sutherland’s model of learning (Sutherland 1959, 1964; Sutherland & Macintosh 1971). A_i is an analyzer that examines stimuli along a stimulus dimension. R is a response unit that can be attached to different analyzers. Solid lines are existing response attachments, dashed lines represent further possible attachments. In this figure, A_1 analyzes brightness and discriminates between black (B) and white (W), whereas A_2 discriminates between horizontal (H) and vertical (V) orientation. Learning is assumed to consist of (1) learning to use analyzers relevant for the discrimination and (2) learning to attach the right response to the relevant analyzers.

So why are neural network models often absent from current animal behavior theory? One reason could be that neural network research emerged mainly from the artificial intelligence community, with a strong focus on humans rather than animals in general. To date, much more neural network research is concerned with humans than with other animals. For instance, James McClelland, one of the most productive scientists in the field, writes

> Connectionist cognitive modeling is an approach to understanding the mechanisms of human cognition through the use of simulated networks of simple, neuronlike processing units. (McClelland 1999; emphasis added)

Without a look to history, the focus on humans does not seem motivated because it is easier to understand the neural basis of behavior in organisms less complex than humans. Differences between research traditions may also have hindered the development of neural network models of animal behavior. Most work in animal behavior is empirical, whereas neural network models emerged from a theoretical research community. Among students of animal behavior, the computer simulation techniques and formal mathematics that are so helpful in exploiting neural network models were not widely available. Terminological barriers might also have contributed. For instance, the term *adaptive* in biology is used strictly to indicate a trait that evolved because it increases individual reproduction (fitness). In engineering and cognitive science the expression *adaptive system* has a broader scope and refers to any system that can change to better serve its purpose. Engineers thus may speak of *adaptation* when biologists would speak of *learning*. Another example is neural network theory referring to *self-organization* where ethologists would talk of *learning* or *development* and experimental psychologists of *perceptual learning*. Important terms such as *reinforcement* and *association* are also used in slightly different ways.

In conclusion, traditional ethological and animal psychological thinking contains a number of seeds to neural network models, but the development of neural network theory has occurred mainly outside these disciplines. Neural network models still have not gained broad popularity in animal behavior research, but there is today a growing interest in neural networks, particularly among animal psychologists.

## 1.4.4 The diversity of network models: Our approach

To apply neural networks to animal behavior, we need to decide which particular models to use. This is not always easy. Neural network models come in many forms and purposes. There are biologically or psychologically motivated models with aims ranging from the very details of neural mechanisms to the highest mental functions in humans. There are models aimed primarily at machine intelligence and engineering applications with little concern for biological realism. The latter nevertheless can be of interest to modeling animal behavior for practical and theoretical reasons. In this book we try to use simple networks as long as they can account for the behavior we investigate. There are a number of reasons for this approach. First, complexity should not be introduced prematurely and without reason. We could try to include from the start all known details of nervous systems, but this would result in a model as difficult to understand as the real system. The only way to understand a complex structure is to start by abstracting pieces from it or study simplified models that are more readily analyzed. The crucial test of a simplified model is the extent to which it captures essential features of the behavior of real animals. If it does, then the fact that the model is neurally inspired rather than based on some other metaphor should be considered a bonus rather than a hindrance.

Second, we need models of animal behavior that are easy to understand and practical to use. We also need general models as opposed to those specific to a particular behavior and a particular species. The subject of animal behavior covers species with a nervous system made up of a few cells to the complexity of primate brains, and we know that many behavioral phenomena are surprisingly general.

Third, the differences between network models should not be exaggerated. Starting from a simple model such as Rosenblatt's *perceptron*, we can add complexity gradually and in several ways. For instance, we can add more layers of nodes, recurrent connections and more complex node dynamics. We thus can obtain complex models gradually from simple ones and study how their properties change in the process. This is also relevant when studying the evolution from simple to complex behavior (Chapter 5).

In practice, our approach means that multilayer feedforward networks operating in discrete time are our first choice of model. Indeed, most applications of neural networks are of this kind. If such models prove insufficient to analyze a given behavioral finding, we consider additional elements such as recurrent connections or dynamics in continuous time. Note that we do not deny the importance of detailed models. If neural network models are to fulfill their promises, the future will contain simple, intuitive, general and practical models, as well as detailed models closer to real nervous systems.

## CHAPTER SUMMARY

- “Behavior” is a legitimate level of analysis. It has theoretical importance in ethology, psychology, behavioral ecology and evolutionary biology and practical importance to many people working and living with animals in zoos, veterinary clinics, farms, etc.
- Explaining behavior includes understanding how motivational factors control responding, how behavior develops during an individual’s lifetime and how evolution shapes behavior. Understanding of actual internal processes may also be important.
- Most attempts to understand animal behavior have inferred models from behavioral observations and functional considerations. This is true for most of ethology, experimental psychology and cognitive psychology. A major exception is neuroethology, which studies how nervous systems generate behavior.
- Neural network models offer a potential to develop models of behavior that are informed not only by behavioral observations but also by the actual structure of nervous systems. Can this result in increased knowledge about behavior? Our aim is to explore this question.
- We have also touched on some fundamental issues about how to model behavior, from neurophysiology to “cognition.” One important issue is how to deal with animals’ internal states. We will return to these issues throughout this book and in the concluding chapter.

## FURTHER READING

Ethological and biological theory of behavior:

- Eibl-Eibesfeldt I, 1975. *Ethology: The Biology of Behavior*. New York: Holt, Rinehart & Winston.
- Hinde RA, 1970. *Animal Behaviour*. Tokyo: McGraw-Hill Kogakusha, 2 edition.
- Krebs JR, Davies NB, 1987. *An Introduction to Behavioural Ecology*. London: Blackwell, 2 edition.
- McFarland DJ, 1999. *Animal Behaviour: Psychobiology, Ethology and Evolution*. Harlow, England: Longman, 3 edition.

Neuroethology:

- Ewert JP, 1985. Concepts in vertebrate neuroethology. *Animal Behaviour* 33, 1–29.
