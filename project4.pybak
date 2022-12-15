#Code Written By: Emmaline Mercer
#Date: 11/28/2022

global noise1
noise1 = 0

global noise2
noise2 = 0

global noise3
noise3 = 0

global noise4
noise4 = 0

global noise5
noise5 = 0

global noise6
noise6 = 0

global noise7
noise7 = 0

global moves
moves = 0    

#main function
def adventure():
  global keyCard, paperwork, moves, radio
  location = "Main Door"
  name = requestString("What is your name: ")
  name = name.upper()
  intro = showIntroduction(name)
  showInformation(intro)
  floorplan = initialization()
  roomActions(name,location)

#actions made for directions and room movements
def roomActions(name, location):
  global keyCard, paperwork, moves, radio
  copyPicture(makePicture(getMediaPath("you.png")), floorplan, 590, 71)
  while not (location == "Exit"): 
    if location == "Control Room" and keyCard != "player":
      showInformation("You need a keycard to open this door. Explore the shuttle some more. ")
      location = "Main Room"
    roomInfo = showRoom(location)
    showInformation(roomInfo)
    pickUpQuestions(location)
    showItems()
    dropQuestions(location)
    showItems()
    if keyCard == "player" and paperwork == "Office" and moves <= 25 and radio == "player":
      call = requestString("You have completed your other tasks. Do you want to radio for help?")
      if call.lower() == "yes": 
        showInformation("Congratulations! You escaped the imposter and won the game!")
        showInformation("Your score is " + str(moves))
        writePlayerNameAndScore(name)
        break
    if moves > 25:
      showInformation("Oh no! You ran out of moves and the imposter killed you! You lost the game!")
      showInformation("Your score is " + str(moves))
      writePlayerNameAndScore(name)
      break
    direction = requestString("Which direction?") 
    print "You typed: " + direction  
    clearItemAreaOfMap()
    location = pickRoom(direction, location, name)
      
#writes all player data to file
def writePlayerNameAndScore(name):
  global moves
  data = playerScore(name, moves)
  reads = getPlayerData()
  print reads
  for player in reads:
    if player[0] == name:
      if player[1] <= moves:
        break
      if player[1] > moves:
        reads.remove(player)
        reads.append(data)
        writeFile(reads)
        break
  if player[0] != name:
    reads.append(data)
    writeFile(reads) 

#player name and score in a list
def playerScore(name, score):
  list = [name, score]
  return list

def removeBlankLines(string):
  while (string.find("\n\n") != -1):      
    string = string.replace("\n\n","\n")
  if(string.startswith("\n")):            
    string = string[1:]
  if(string.endswith("\n")):              
    string = string[:len(string) - 1]
  return string

def getPlayerData():
  raw_data = readFile()
  raw_data = removeBlankLines(raw_data)
  player_list = raw_data.split("\n")
  player_list.sort()
  player_data = []
  for player in player_list:
    player = player.split(":")
    player_data = player_data + [[player[0], int(player[1])]]
  return player_data

def readFile():
  filepicked = getMediaPath("Project4_Scores.txt")
  file = open(filepicked, "rt")
  fileString = file.read()
  file.close()
  return fileString

def writeFile(reads):
  new_data = ""
  for player in reads:
    new_data = new_data + player[0] + ":" + str(player[1]) + "\n"
  file = open(getMediaPath("Project4_Scores.txt"), "wt")
  file.write(new_data)
  file.close()
  
def initialization():
    global keyCard, paperwork, radio, floorplan
    keyCard = "Lounge"
    paperwork = "Control Room"
    radio = "Engine Room"
    floorplan = makePicture(getMediaPath("floorplan.jpg"))
    repaint(floorplan)
  
def pickUpQuestions(room):
    global keyCard, paperwork, radio
    if keyCard == room:
        q = requestString("You found a keycard. Do you want to pick it up?")
        if q.lower() == "yes":
            keyCard = "player"
    if paperwork == room and keyCard == "player":
        q = requestString("You found a bunch of paperwork. Do you want to pick it up?")
        if q.lower() == "yes":
            paperwork = "player"
    if radio == room:
        q = requestString("You found a hand-held radio. Do you want to pick it up?")
        if q.lower() == "yes":
            radio = "player"
   
def showItems():
    global keyCard, paperwork, radio, floorplan
    src = makePicture(getMediaPath("keycard.jpg"))
    src2 = makePicture(getMediaPath("paperwork.jpg"))
    src3 = makePicture(getMediaPath("radio.jpg"))
    if keyCard == "player":
        copyPicture(src, floorplan, 56, 476)
    if paperwork == "player":
        copyPicture(src2, floorplan, 200, 476)
    if radio == "player":
        copyPicture(src3, floorplan, 432, 455)
    repaint(floorplan)

def clearItemAreaOfMap():
  global floorplan
  for x in range(42, 490):
    for y in range(69, 369):
      setColor(getPixel(floorplan, x, y), white)
      
def clearItemAreaOfMap2():
  global floorplan
  for x in range(39, 190):
    for y in range(469, 615):
      setColor(getPixel(floorplan, x, y), white)
      
def clearItemAreaOfMap3():
  global floorplan
  for x in range(190, 420):
    for y in range(471, 615):
      setColor(getPixel(floorplan, x, y), white)
      
def clearItemAreaOfMap4():
  global floorplan
  for x in range(430, 604):
    for y in range(447, 615):
      setColor(getPixel(floorplan, x, y), white)

def copyPicture(source, target, targetX, targetY):
  for sourceX in range(0, getWidth(source)):
    for sourceY in range(0, getHeight(source)):
      color = getColor(getPixel(source, sourceX, sourceY))
      setColor(getPixel(target, sourceX+targetX, sourceY+targetY), color)
  
def dropQuestions(room):
    global keyCard, paperwork, radio
    if keyCard == "player":
      q = requestString("Do you want to drop the keycard?")
      if q.lower() == "yes":
        keyCard = room
        clearItemAreaOfMap2()
    if paperwork == "player" and room != "Office":
      q = requestString("Do you want to drop the paperwork?")
      if q.lower() == "yes":
        paperwork = room
        clearItemAreaOfMap3()
    if paperwork == "player" and room == "Office":
      q = requestString("You need to organize the paperwork and leave it in the office. Do you want to drop the paperwork?")
      if q.lower() == "yes":
        paperwork = room
        clearItemAreaOfMap3()
    if radio == "player":
      q = requestString("Do you want to drop the radio?")
      if q.lower() == "yes":
        radio = room
        clearItemAreaOfMap4()

#introduction
def showIntroduction(name):
  a = "You are the last survivor on the infamous SUS2000 space craft . . . " 
  b = "Your whole crew has been mysteriously murdered, "
  c = "and you don't know who did it. "
  e = "In each room, you will be told " 
  f = "which directions you can go. "
  g = "You can move north, south, east, or west "
  h = "by typing that direction. "
  i = "You must complete 3 tasks in order to escape the imposter: "
  j = "Get the keycard and use it, drop the paperwork in the office, "
  k = "and get the radio and use it to call for help. "
  l = "You must complete the game in 25 moves or less or else the imposter will find you "
  m = "and you lose the game. "
  n = "Type help to replay this introduction. "
  o = "Type quit or exit to end the program. "
  p = "Type score to see your score. Your score is determined based on the number of moves you use. "
  q = "Like golf, the lower your score the better. "
  r = "Type scoreboard to see all the previous players and their scores. "
  s = "Good luck, space ranger " + name + "." + " You're going to need it. "
  return a + b + c + e + f + g + h + i + j + k + l + m + n + o + p + q + r + s

#shows the room the user chooses
def showRoom(room):
  global floorplan
  printNow("===========")
  if room == "Main Door":
    a = showMainDoor()
    return a
  if room == "Lounge":
    a = showLounge(room)
    return a
  if room == "Engine Room":
    a = showEngineRoom(room)
    return a
  if room == "Kitchen":
    a = showKitchen()
    return a
  if room == "Office":
    a = showOffice(room)
    return a
  if room == "Main Room":
    a = showMainRoom()
    return a
  if room == "Control Room":  
    a = showControlRoom(room)
    return a
  

#follows the directions of the user to find a room
def pickRoom(direction, room, name):
  global moves, keyCard
  if (direction == "quit") or (direction == "exit"):
    showInformation("You abandoned the mission. Goodbye coward!") 
    return "Exit" 
  if direction == "help": 
    showInformation(showIntroduction(name)) 
    return room     
  if direction == "score":
    showInformation(name + ":" + str(moves))
    return room
  if direction == "scoreboard":
    players = readFile()
    showInformation(players)
    return room
  if room == "Main Door": 
    if direction == "north": 
      return "Main Room"
    if direction == "east": 
      return "Kitchen" 
    if direction == "west": 
      return "Lounge"  
  if room == "Main Room":
    if direction == "north": 
      return "Control Room" 
    if direction == "south": 
      return "Main Door"
  if room == "Kitchen": 
    if direction == "north": 
      return "Office"
    if direction == "south":
      return "Main Door"
  if room == "Office": 
    if direction == "south": 
      return "Kitchen" 
  if room == "Lounge": 
    if direction == "north": 
      return "Engine Room"
    if direction == "south": 
      return "Main Door" 
  if room == "Engine Room":   
    if direction == "south":
      return "Lounge" 
  if room == "Control Room":
    if direction == "south":
      return "Main Room"
     
  showInformation("You can't (or don't want to) go in that direction")
  return room
  
def showMainDoor():
  global floorplan, moves, noise7
  if moves != 0:
    moves = moves + 1
  copyPicture(makePicture(getMediaPath("main_door.jpg")), floorplan, 61, 98)
  repaint(floorplan)
  a = "You are in the main door room that leads into the space shuttle. " 
  b = "There are three glowing, futuristic doors around you. "
  c = "One on your left to the west, one in front of you to the north, and one on your right to the east. "
  d = "Choose a door to travel deeper into the space shuttle. "
  if noise7 == 0:
    sound = makeSound(getMediaPath("main_door.wav"))
    blockingPlay(sound)
    noise7 = 1
  return a + b + c + d

def showMainRoom():
  global floorplan, noise1, moves
  moves = moves + 1
  copyPicture(makePicture(getMediaPath("main-room.jpg")), floorplan, 61, 98)
  repaint(floorplan)
  a = "You are now in the main room of the shuttle. " 
  b = "The sleek, white design of the room surrounds you, and you feel a sense of unease.  "
  c = "There are dark corners everywhere . . . "
  d = "You can return to the main door in the south, "
  e = "or continue onward by going north. "
  f = "Choose wisely . . . "
  if noise1 == 0:
    sound = makeSound(getMediaPath("spacedoor.wav"))
    blockingPlay(sound)
    noise1 = 1
  return a + b + c + d + e + f
  
def showControlRoom(room):
  global paperwork, floorplan, noise2, keyCard, moves
  moves = moves + 1
  copyPicture(makePicture(getMediaPath("control_tower.jpg")), floorplan, 61, 98)
  repaint(floorplan)
  a = "You have entered the control room. " 
  b = "A plethera of machinery and futuristic automation engulf you and make you feel small. "
  c = "There are blinking lights and beeping sounds coming from a few of the computers. "
  d = "You can return to the main room by going south. "
  if noise2 == 0:
    sound = makeSound(getMediaPath("computer.wav"))
    blockingPlay(sound)
    noise2 = 1
  return a + b + c + d 
  
def showLounge(room):
  global keyCard, floorplan, noise3, moves
  moves = moves + 1
  copyPicture(makePicture(getMediaPath("lounge.jpg")), floorplan, 61, 98)
  repaint(floorplan)
  a = "You are in the lounge. " 
  b = "Some cozy chairs and a couch are organized into a unique seating arrangment.  "
  c = "There are pictures of earth and your crewmate's families covering the walls. "
  d = "You miss your crewmates . . . "
  e = "You can continue north, or return to the main door by going south. "
  if noise3 == 0:
    sound = makeSound(getMediaPath("doorLounge.wav"))
    blockingPlay(sound)
    noise3 = 1
  return a + b + c + d + e

def showKitchen():
  global floorplan, noise4, moves
  moves = moves + 1
  copyPicture(makePicture(getMediaPath("kitchen.jpg")), floorplan, 61, 98)
  repaint(floorplan)
  a = "You have entered the kitchen. " 
  b = "White drawers and cabinets surround the room, and futuristic machines "
  c = "are ready to prepare any meal you desire. "
  d = "The room is cold and empty.  "
  e = "You can return to the main door by going south, or continue onward by going north. "
  if noise4 == 0:
    sound = makeSound(getMediaPath("dishes.wav"))
    blockingPlay(sound)
    noise4 = 1
  return a + b + c + d + e

def showOffice(room):
  global floorplan, noise5, moves, paperwork
  moves = moves + 1
  copyPicture(makePicture(getMediaPath("office.jpg")), floorplan, 61, 98)
  repaint(floorplan)
  a = "You are now inside the office. " 
  c = "You don't recall the last time you worked on some paperwork. "
  d = "It was always your least favorite task. "
  e = "However, you need to organize the paperwork by dropping it in the office. "
  f = "You can return to the kitchen by going south."
  if noise5 == 0:
    sound = makeSound(getMediaPath("doorOffice.wav"))
    blockingPlay(sound)
    noise5 = 1   
  return a + c + d + e + f

def showEngineRoom(room):
  global floorplan, noise6, moves, keyCard, paperwork, radio
  moves = moves + 1
  copyPicture(makePicture(getMediaPath("engine_room.jpg")), floorplan, 61, 98)
  repaint(floorplan)
  a = "You have entered the engine room. " 
  b = "It's loud and chaotic, but you find peace in the noise drowning out your thoughts. "
  c = "You can return to the lounge by going south. "
  if noise6 == 0:
    sound = makeSound(getMediaPath("machine.wav"))
    blockingPlay(sound)
    noise6 = 1
  return a + b + c
  