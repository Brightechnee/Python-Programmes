# Python-Programmes
#Python programes for practice
#Hangman with basic  graphics and 7 chances 

#Start of the code
words = ["aback","abaft","abandoned","abashed","aberrant","abhorrent","abiding","abject","ablaze","able","abnormal","aboard","aboriginal","abortive","abounding","abrasive","abrupt","absent","absorbed","absorbing","abstracted","absurd","abundant","abusive","acceptable","accessible","accidental","accurate","acid","acidic","acoustic","acrid","actually","ad hoc","adamant","adaptable","addicted","adhesive","adjoining","adorable","adventurous","afraid","aggressive","agonizing","agreeable","ahead","ajar","alcoholic","alert","alike","alive","alleged","alluring","aloof","amazing","ambiguous","ambitious","amuck","amused","amusing","ancient","angry","animated","annoyed","annoying","anxious","apathetic","aquatic","aromatic","arrogant","ashamed","aspiring","assorted","astonishing","attractive","auspicious","automatic","available","average","awake","aware","awesome","awful","axiomatic","bad","barbarous","bashful","bawdy","beautiful","befitting","belligerent","beneficial","bent","berserk","best","better","bewildered","big","billowy","bite-sized","bitter","bizarre","black","black-and-white","bloody","blue","blue-eyed","blushing","boiling","boorish","bored","boring","bouncy","boundless","brainy","brash","brave","brawny","breakable","breezy","brief","bright","bright","broad","broken","brown","bumpy","burly","bustling","busy","cagey","calculating","callous","calm","capable","capricious","careful","careless","caring","cautious","ceaseless","certain"]


import random
import string 


graphic = {
        0: """
                ___________
               | /        | 
               |/        ( )
               |          |
               |         / \\
               |
           """,
        1: """
                ___________
               | /        | 
               |/        ( )
               |          |
               |         / 
               |
            """,
        2: """
                ___________
               | /        | 
               |/        ( )
               |          |
               |          
               |
            """,
        3: """
                ___________
               | /        | 
               |/        ( )
               |          
               |          
               |
            """,
        4: """
                ___________
               | /        | 
               |/        
               |          
               |          
               |
            """,
        5: """
                ___________
               | /        
               |/        
               |          
               |          
               |
            """,
        6: """
               |
               |
               |
               |
               |
            """,
        7: "",
    }


def get_valid_word(words):
  
  word = random.choice(words)
  while "-" in word or " " in word or "_" in word:
     word = random.choice(words)
 
  return word.upper()
  
  
def hangman():
  
  word = get_valid_word(words)
  word_letters = set( word)
  possible_letters = set(string.ascii_uppercase)
  used_letters = set()
  
  
  lives = 7
  #have the user input a letter
  #compare teh letter to the letters of a given word
  #if the letter matches, add it to the word_guess
  #if not, subtract a life
  #while life > 0, keep running the loop
  #when life = 0, print a failure message
  #If the letter was already guessed, print a message saying you have already used the letter unless it is still required in the word(Multiple similar letters.)
  
  while len(word_letters) > 0 and lives > -1:
    
    print(graphic[lives])
    print("You have", lives, "lives left and you have used the following letters:"," " .join(used_letters))
  
  
    #This part of the code updates you on your progress
    word_update = [(letter if letter in used_letters else "_" )for letter in word]
    print ("Word Progress: ", " " .join(word_update))
  
  
    guess = input("Guess a letter: ").upper()
    
    if guess in possible_letters - used_letters:
      used_letters.add(guess)
      if guess in word_letters:
        word_letters.remove(guess)
        print("")
        
      else:
        lives = lives-1
        print("\nYour letter, %s, is not in the word." %guess)
    elif guess in used_letters:
      print("\nYou have already used this letter. Try again")
    
    else:
      print("That is not a valid character. Try again")
      
  if lives == -1:
    print("You ran out of chances. Try another word. The word was:" , word)
    
  elif len(word_letters) ==0:
    print("Yaay, You guessed the word:", word, "correctly")
    
hangman()
