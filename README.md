<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>English Crossword — 800 Essential Words</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Segoe UI',Arial,sans-serif;background:#FFF8EE;min-height:100vh;padding:16px}
header{text-align:center;margin-bottom:16px}
header h1{font-size:26px;font-weight:700;color:#534AB7;letter-spacing:.5px}
header p{font-size:13px;color:#854F0B;margin-top:4px}
#cw-wrap{display:flex;gap:16px;flex-wrap:wrap;justify-content:center;align-items:flex-start}
#board-section{display:flex;flex-direction:column;align-items:center;gap:10px}
#toolbar{display:flex;gap:8px;flex-wrap:wrap;justify-content:center}
.btn{font-size:13px;padding:7px 18px;border-radius:20px;border:2px solid #AFA9EC;background:#EEEDFE;color:#3C3489;cursor:pointer;font-weight:600;transition:background .15s}
.btn:hover{background:#CECBF6}
.btn.primary{background:#7F77DD;color:#fff;border-color:#534AB7}
.btn.primary:hover{background:#534AB7}
.dir-row{display:flex;gap:6px}
.dir-btn{font-size:13px;padding:5px 16px;border-radius:20px;border:1.5px solid #AFA9EC;background:transparent;color:#534AB7;cursor:pointer;font-weight:600}
.dir-btn.on{background:#EEEDFE;border-color:#7F77DD;color:#3C3489}
#board-wrap{background:#FAEEDA;border-radius:18px;padding:14px;border:3px solid #EF9F27}
#cw-grid{display:grid;gap:3px}
.cw-cell{width:48px;height:48px;position:relative;border-radius:8px;border:2px solid #EF9F27;background:#fffdf5;cursor:pointer;display:flex;align-items:center;justify-content:center}
.cw-cell.blocked{background:#EF9F27;border-color:#BA7517;cursor:default;border-radius:6px}
.cw-cell.active{outline:3px solid #534AB7;z-index:2;background:#EEEDFE}
.cw-cell.highlight{background:#FFF3C4}
.cw-cell.correct{background:#EAF3DE;border-color:#639922}
.cw-cell.wrong{background:#FCEBEB;border-color:#E24B4A}
.cw-num{position:absolute;top:2px;left:3px;font-size:11px;font-weight:700;line-height:1;color:#412402;background:rgba(255,255,255,0.85);border-radius:3px;padding:0 2px;pointer-events:none;z-index:3}
.cw-cell.active .cw-num{color:#26215C;background:rgba(238,237,254,0.95)}
.cw-cell.correct .cw-num{color:#173404;background:rgba(234,243,222,0.95)}
.cw-cell.wrong .cw-num{color:#501313;background:rgba(252,235,235,0.95)}
.cw-cell input{width:100%;height:100%;border:none;background:transparent;text-align:center;font-size:23px;font-weight:700;text-transform:uppercase;outline:none;color:#26215C;cursor:pointer;padding:10px 0 0 0}
.cw-cell.active input{color:#3C3489}
#cw-msg{font-size:15px;font-weight:700;min-height:24px;text-align:center;padding:4px 0}
#cw-msg.success{color:#27500A}
#cw-msg.error{color:#A32D2D}
#cw-msg.info{color:#185FA5}
#cw-prog{font-size:12px;color:#854F0B;text-align:center}
#clue-panel{width:240px;display:flex;flex-direction:column;gap:10px;max-height:540px;overflow-y:auto}
.clue-box{background:#E1F5EE;border-radius:14px;border:2px solid #5DCAA5;padding:10px 12px}
.clue-box h3{font-size:12px;font-weight:700;margin:0 0 7px;color:#085041;text-transform:uppercase;letter-spacing:.07em}
.clue-item{font-size:13px;padding:5px 7px;border-radius:8px;cursor:pointer;display:flex;gap:6px;line-height:1.4;margin-bottom:2px;color:#085041}
.clue-item:hover{background:#9FE1CB}
.clue-item.active-clue{background:#5DCAA5;color:#04342C;font-weight:700}
.clue-item.done-clue{color:#0F6E56;text-decoration:line-through;opacity:.55}
.clue-num{font-weight:700;min-width:20px;color:#0F6E56;flex-shrink:0}
.clue-ko{font-size:11px;opacity:.75}
footer{text-align:center;margin-top:20px;font-size:11px;color:#BA7517;opacity:.7}
@media(max-width:600px){
  #clue-panel{width:100%;max-height:260px}
  .cw-cell{width:40px;height:40px}
  .cw-cell input{font-size:19px}
}
</style>
</head>
<body>
<header>
  <h1>★ English Crossword ★</h1>
  <p>800 Essential Words for Elementary Students</p>
</header>
<div id="cw-wrap">
  <div id="board-section">
    <div id="toolbar">
      <button class="btn" id="btn-check">✓ Check</button>
      <button class="btn" id="btn-reveal">👁 Reveal</button>
      <button class="btn primary" id="btn-new">↺ New Puzzle</button>
    </div>
    <div class="dir-row">
      <button class="dir-btn on" id="btn-across">→ Across</button>
      <button class="dir-btn" id="btn-down">↓ Down</button>
    </div>
    <div id="board-wrap">
      <div id="cw-grid"></div>
    </div>
    <div id="cw-msg"></div>
    <div id="cw-prog"></div>
  </div>
  <div id="clue-panel">
    <div class="clue-box"><h3>→ Across</h3><div id="clues-across"></div></div>
    <div class="clue-box"><h3>↓ Down</h3><div id="clues-down"></div></div>
  </div>
</div>
<footer>Words from the 800 Essential English Vocabulary for Elementary School &nbsp;|&nbsp; Click a cell to select · Click again to switch direction</footer>
<script>
const POOL=[{"w":"EAR","m":"귀"},{"w":"HAIR","m":"머리카락"},{"w":"QUEEN","m":"여왕"},{"w":"TABLE","m":"식탁"},{"w":"WAIT","m":"기다리다"},{"w":"CAKE","m":"케이크"},{"w":"EARLY","m":"일찍"},{"w":"HALF","m":"절반"},{"w":"CALL","m":"부르다"},{"w":"EARTH","m":"지구"},{"w":"MAIL","m":"우편"},{"w":"QUICK","m":"빠른"},{"w":"TALK","m":"말하다"},{"w":"WALK","m":"걷다"},{"w":"ACT","m":"행동"},{"w":"CAMERA","m":"사진기"},{"w":"EAST","m":"동쪽"},{"w":"MAKE","m":"만들다"},{"w":"QUIET","m":"조용한"},{"w":"TALL","m":"키가큰"},{"w":"WALL","m":"벽"},{"w":"CAMP","m":"야영지"},{"w":"EASY","m":"쉬운"},{"w":"HAND","m":"손"},{"w":"MAN","m":"사람"},{"w":"TAPE","m":"테이프"},{"w":"WANT","m":"원하다"},{"w":"CAN","m":"할수있다"},{"w":"EAT","m":"먹다"},{"w":"MANY","m":"많은"},{"w":"RAIN","m":"비"},{"w":"TASTE","m":"맛보다"},{"w":"WAR","m":"전쟁"},{"w":"CANDLE","m":"양초"},{"w":"EGG","m":"계란"},{"w":"HAPPY","m":"행복한"},{"w":"MAP","m":"지도"},{"w":"WARM","m":"따뜻한"},{"w":"CANDY","m":"사탕"},{"w":"EMPTY","m":"텅빈"},{"w":"MILK","m":"우유"},{"w":"WASH","m":"씻다"},{"w":"CAP","m":"모자"},{"w":"END","m":"끝"},{"w":"HARD","m":"단단한"},{"w":"TEACH","m":"가르치다"},{"w":"AGE","m":"나이"},{"w":"ENJOY","m":"즐기다"},{"w":"HATE","m":"미워하다"},{"w":"READ","m":"읽다"},{"w":"TEAM","m":"팀"},{"w":"WATCH","m":"보다"},{"w":"AIR","m":"공기"},{"w":"CAR","m":"자동차"},{"w":"ENOUGH","m":"충분한"},{"w":"HAVE","m":"가지고있다"},{"w":"WATER","m":"물"},{"w":"CARD","m":"카드"},{"w":"ERASER","m":"지우개"},{"w":"MEAT","m":"고기"},{"w":"RED","m":"빨강"},{"w":"TELL","m":"이야기하다"},{"w":"CARE","m":"걱정"},{"w":"EVENING","m":"저녁"},{"w":"HEAD","m":"머리"},{"w":"MEDAL","m":"메달"},{"w":"TEMPLE","m":"절"},{"w":"WEAK","m":"약한"},{"w":"CARRY","m":"나르다"},{"w":"EVERY","m":"모든"},{"w":"HEAR","m":"듣다"},{"w":"MEET","m":"만나다"},{"w":"REPEAT","m":"반복하다"},{"w":"TENNIS","m":"테니스"},{"w":"WEAR","m":"옷을입다"},{"w":"CASE","m":"경우"},{"w":"HEART","m":"마음"},{"w":"MELON","m":"멜론"},{"w":"REST","m":"휴식"},{"w":"TEST","m":"시험"},{"w":"ALWAYS","m":"항상"},{"w":"HEAVY","m":"무거운"},{"w":"THANK","m":"감사하다"},{"w":"WEEK","m":"한주"},{"w":"CAT","m":"고양이"},{"w":"HELLO","m":"여보세요"},{"w":"MIDDLE","m":"한가운데"},{"w":"WELCOME","m":"환영하다"},{"w":"CATCH","m":"붙잡다"},{"w":"HELP","m":"돕다"},{"w":"RIBBON","m":"리본"},{"w":"THAT","m":"그것"},{"w":"WELL","m":"상당히"},{"w":"CENTER","m":"중앙"},{"w":"EYE","m":"눈"},{"w":"RICE","m":"쌀"},{"w":"WEST","m":"서쪽"},{"w":"CHAIR","m":"의자"},{"w":"MIRROR","m":"거울"},{"w":"RIDE","m":"타다"},{"w":"THERE","m":"그곳에"},{"w":"CHANCE","m":"기회"},{"w":"FACE","m":"얼굴"},{"w":"HIGH","m":"높은"},{"w":"MODEL","m":"모형"},{"w":"RING","m":"반지"},{"w":"THICK","m":"두꺼운"},{"w":"APPLE","m":"사과"},{"w":"CHANGE","m":"바꾸다"},{"w":"FAIR","m":"공정한"},{"w":"RIVER","m":"강"},{"w":"THIN","m":"얇은"},{"w":"CHEAP","m":"값싼"},{"w":"FALL","m":"가을"},{"w":"HILL","m":"언덕"},{"w":"MONEY","m":"돈"},{"w":"ROAD","m":"길"},{"w":"THINK","m":"생각하다"},{"w":"WHITE","m":"백색"},{"w":"CHEESE","m":"치즈"},{"w":"FAMILY","m":"가족"},{"w":"HIT","m":"때리다"},{"w":"MONKEY","m":"원숭이"},{"w":"ROBOT","m":"로봇"},{"w":"CHICKEN","m":"닭"},{"w":"FAR","m":"멀리"},{"w":"HOLD","m":"잡다"},{"w":"MONTH","m":"달"},{"w":"ROCK","m":"바위"},{"w":"WIDE","m":"넓은"},{"w":"FAST","m":"빠른"},{"w":"HOLIDAY","m":"휴일"},{"w":"MORNING","m":"아침"},{"w":"WILL","m":"할것이다"},{"w":"CHURCH","m":"교회"},{"w":"FAT","m":"뚱뚱한"},{"w":"HOME","m":"집"},{"w":"MOTHER","m":"어머니"},{"w":"ROOF","m":"지붕"},{"w":"THROW","m":"던지다"},{"w":"WIN","m":"이기다"},{"w":"CIRCLE","m":"원"},{"w":"FAMOUS","m":"유명한"},{"w":"HOPE","m":"희망"},{"w":"ROOM","m":"방"},{"w":"TICKET","m":"표"},{"w":"WIND","m":"바람"},{"w":"CITY","m":"도시"},{"w":"FATHER","m":"아버지"},{"w":"MOUTH","m":"입"},{"w":"ROUND","m":"둥근"},{"w":"TIE","m":"매다"},{"w":"WINDOW","m":"창문"},{"w":"CLASS","m":"학급"},{"w":"FEEL","m":"느끼다"},{"w":"MOVE","m":"움직이다"},{"w":"TIGER","m":"호랑이"},{"w":"WING","m":"날개"},{"w":"FEW","m":"조금"},{"w":"MOVIE","m":"영화"},{"w":"RULER","m":"자"},{"w":"WINTER","m":"겨울"},{"w":"CLEAN","m":"깨끗한"},{"w":"FIELD","m":"들판"},{"w":"HORSE","m":"말"},{"w":"RUN","m":"달리다"},{"w":"TIME","m":"시간"},{"w":"CLIMB","m":"오르다"},{"w":"FIGHT","m":"싸움"},{"w":"TIRED","m":"피곤한"},{"w":"WOMAN","m":"여자"},{"w":"CLOCK","m":"시계"},{"w":"FILL","m":"채우다"},{"w":"HOT","m":"뜨거운"},{"w":"MUCH","m":"많은"},{"w":"SAD","m":"슬픈"},{"w":"WONDER","m":"놀라다"},{"w":"BAG","m":"가방"},{"w":"CLOSE","m":"닫다"},{"w":"FILM","m":"필름"},{"w":"HOTEL","m":"호텔"},{"w":"MUSIC","m":"음악"},{"w":"SAFE","m":"안전한"},{"w":"TODAY","m":"오늘"},{"w":"WOOD","m":"나무"},{"w":"BALL","m":"공"},{"w":"CLOUD","m":"구름"},{"w":"FIND","m":"찾다"},{"w":"HOUR","m":"시간"},{"w":"SALT","m":"소금"},{"w":"WORD","m":"낱말"},{"w":"BALLOON","m":"풍선"},{"w":"FINE","m":"좋은"},{"w":"HOUSE","m":"집"},{"w":"SALAD","m":"샐러드"},{"w":"TOMATO","m":"토마토"},{"w":"WORK","m":"일"},{"w":"BANANA","m":"바나나"},{"w":"CLUB","m":"클럽"},{"w":"FINGER","m":"손가락"},{"w":"HOW","m":"어떻게"},{"w":"NAME","m":"이름"},{"w":"SAME","m":"같은"},{"w":"WORLD","m":"세상"},{"w":"BAND","m":"끈"},{"w":"COAT","m":"코트"},{"w":"FINISH","m":"끝내다"},{"w":"NARROW","m":"좁은"},{"w":"SAND","m":"모래"},{"w":"TONIGHT","m":"오늘밤"},{"w":"WRITE","m":"쓰다"},{"w":"BANK","m":"은행"},{"w":"COFFEE","m":"커피"},{"w":"FIRE","m":"불"},{"w":"HUNGRY","m":"배고픈"},{"w":"NEAR","m":"가까운"},{"w":"SAY","m":"말하다"},{"w":"WRONG","m":"나쁜"},{"w":"BASE","m":"기초"},{"w":"COIN","m":"동전"},{"w":"FISH","m":"물고기"},{"w":"HURRY","m":"서두르다"},{"w":"NECK","m":"목"},{"w":"SCHOOL","m":"학교"},{"w":"TOOTH","m":"이"},{"w":"BASKET","m":"바구니"},{"w":"COLD","m":"추운"},{"w":"HURT","m":"다치다"},{"w":"NEED","m":"필요하다"},{"w":"SCORE","m":"점수"},{"w":"TOP","m":"꼭대기"},{"w":"YEAR","m":"한해"},{"w":"BATH","m":"목욕"},{"w":"COLOR","m":"색깔"},{"w":"FLAG","m":"깃발"},{"w":"NEVER","m":"결코않다"},{"w":"SEA","m":"바다"},{"w":"TOUCH","m":"만지다"},{"w":"YELLOW","m":"노랑색"},{"w":"COME","m":"오다"},{"w":"FLOOR","m":"마루"},{"w":"NEW","m":"새로운"},{"w":"SEASON","m":"계절"},{"w":"TOWN","m":"도시"},{"w":"BEACH","m":"해변"},{"w":"FLOWER","m":"꽃"},{"w":"ICE","m":"얼음"},{"w":"NEWS","m":"뉴스"},{"w":"SEAT","m":"의자"},{"w":"TOY","m":"인형"},{"w":"BEAR","m":"곰"},{"w":"COOK","m":"요리하다"},{"w":"FLY","m":"날다"},{"w":"IDEA","m":"생각"},{"w":"NEXT","m":"다음의"},{"w":"SEE","m":"보다"},{"w":"TRAIN","m":"기차"},{"w":"COOL","m":"시원한"},{"w":"FOLLOW","m":"따르다"},{"w":"NICE","m":"좋은"},{"w":"SELL","m":"팔다"},{"w":"TRAVEL","m":"여행하다"},{"w":"COPY","m":"복사"},{"w":"FOOD","m":"음식"},{"w":"NIGHT","m":"밤"},{"w":"SEND","m":"보내다"},{"w":"TREE","m":"나무"},{"w":"BECOME","m":"되다"},{"w":"CORNER","m":"모퉁이"},{"w":"FOOL","m":"바보"},{"w":"NOTE","m":"공책"},{"w":"TRIP","m":"여행"},{"w":"YOUNG","m":"젊은"},{"w":"BED","m":"침대"},{"w":"COUNT","m":"세다"},{"w":"FOOT","m":"발"},{"w":"INK","m":"잉크"},{"w":"NOISE","m":"소음"},{"w":"SET","m":"놓다"},{"w":"TRUCK","m":"화물차"},{"w":"COUNTRY","m":"지역"},{"w":"NORTH","m":"북쪽"},{"w":"TRUE","m":"참된"},{"w":"ZERO","m":"영"},{"w":"BEGIN","m":"시작하다"},{"w":"COURSE","m":"과정"},{"w":"FORGET","m":"잊다"},{"w":"NOSE","m":"코"},{"w":"SHAPE","m":"모양"},{"w":"TRY","m":"노력하다"},{"w":"ZOO","m":"동물원"},{"w":"BEHIND","m":"뒤에"},{"w":"COUSIN","m":"사촌"},{"w":"FORK","m":"포크"},{"w":"SHUT","m":"닫다"},{"w":"BELL","m":"종"},{"w":"COVER","m":"덮다"},{"w":"FREE","m":"자유로운"},{"w":"ISLAND","m":"섬"},{"w":"SHEEP","m":"양"},{"w":"TURN","m":"돌다"},{"w":"BELOW","m":"아래"},{"w":"COW","m":"암소"},{"w":"FRESH","m":"신선한"},{"w":"NOW","m":"지금"},{"w":"SHEET","m":"시트"},{"w":"TWICE","m":"두번"},{"w":"BENCH","m":"긴의자"},{"w":"CRAYON","m":"크레파스"},{"w":"FRIEND","m":"친구"},{"w":"NUMBER","m":"숫자"},{"w":"SHIP","m":"배"},{"w":"CREAM","m":"크림"},{"w":"JOB","m":"직업"},{"w":"NURSE","m":"간호원"},{"w":"SHIRT","m":"셔츠"},{"w":"CROSS","m":"가로지르다"},{"w":"FRONT","m":"앞"},{"w":"JOIN","m":"가입하다"},{"w":"SHOE","m":"구두"},{"w":"UNCLE","m":"삼촌"},{"w":"BICYCLE","m":"자전거"},{"w":"CRY","m":"울다"},{"w":"FRUIT","m":"과일"},{"w":"JUICE","m":"주스"},{"w":"SHOOT","m":"쏘다"},{"w":"UNDER","m":"아래에서"},{"w":"BIG","m":"큰"},{"w":"CUP","m":"컵"},{"w":"FULL","m":"가득찬"},{"w":"JUMP","m":"뛰어오르다"},{"w":"SHOP","m":"가게"},{"w":"BIRD","m":"새"},{"w":"FUN","m":"즐거움"},{"w":"JUNGLE","m":"밀림"},{"w":"SHORT","m":"짧은"},{"w":"JUST","m":"오직"},{"w":"OFFICE","m":"사무실"},{"w":"BLACK","m":"검정색"},{"w":"DANCE","m":"춤추다"},{"w":"GAME","m":"놀이"},{"w":"OFTEN","m":"종종"},{"w":"SHOUT","m":"외치다"},{"w":"USE","m":"사용하다"},{"w":"BLOW","m":"불다"},{"w":"GARDEN","m":"정원"},{"w":"KEEP","m":"지키다"},{"w":"SHOW","m":"보이다"},{"w":"BLUE","m":"푸른"},{"w":"DARK","m":"어두운"},{"w":"GAS","m":"가스"},{"w":"KEY","m":"열쇠"},{"w":"OIL","m":"기름"},{"w":"SHOWER","m":"소나기"},{"w":"BOARD","m":"판자"},{"w":"DATE","m":"날짜"},{"w":"GATE","m":"문"},{"w":"KICK","m":"차다"},{"w":"SICK","m":"아픈"},{"w":"BOAT","m":"배"},{"w":"GENTLE","m":"온화한"},{"w":"KID","m":"아이"},{"w":"OLD","m":"늙은"},{"w":"BODY","m":"몸"},{"w":"DAY","m":"낮"},{"w":"GET","m":"얻다"},{"w":"KILL","m":"죽이다"},{"w":"SIDE","m":"옆"},{"w":"VERY","m":"대단히"},{"w":"BOOK","m":"책"},{"w":"DEAD","m":"죽은"},{"w":"GIRL","m":"소녀"},{"w":"KIND","m":"친절한"},{"w":"ONCE","m":"한번"},{"w":"SIGN","m":"기호"},{"w":"BOTTLE","m":"병"},{"w":"DEEP","m":"깊은"},{"w":"GIVE","m":"주다"},{"w":"KING","m":"왕"},{"w":"ONLY","m":"오직"},{"w":"SILVER","m":"은"},{"w":"BOWL","m":"사발"},{"w":"DEAR","m":"존경하는"},{"w":"GLAD","m":"기쁜"},{"w":"KITCHEN","m":"부엌"},{"w":"OPEN","m":"열린"},{"w":"SING","m":"노래하다"},{"w":"VISIT","m":"방문하다"},{"w":"BOX","m":"상자"},{"w":"DESK","m":"책상"},{"w":"GLASS","m":"유리"},{"w":"KNEE","m":"무릎"},{"w":"VIOLIN","m":"바이올린"},{"w":"BOY","m":"소년"},{"w":"GLOVE","m":"장갑"},{"w":"KNIFE","m":"칼"},{"w":"ORANGE","m":"오렌지"},{"w":"SISTER","m":"자매"},{"w":"BREAD","m":"빵"},{"w":"DIARY","m":"일기"},{"w":"KNOCK","m":"두드리다"},{"w":"OTHER","m":"그밖의"},{"w":"SIT","m":"앉다"},{"w":"BREAK","m":"깨뜨리다"},{"w":"KNOW","m":"알다"},{"w":"SIZE","m":"크기"},{"w":"GOLD","m":"금"},{"w":"SKATE","m":"스케이트"},{"w":"BRIDGE","m":"다리"},{"w":"DINNER","m":"저녁"},{"w":"GOOD","m":"좋은"},{"w":"LADY","m":"숙녀"},{"w":"SKIRT","m":"치마"},{"w":"BRIGHT","m":"밝은"},{"w":"DIRTY","m":"더러운"},{"w":"LAKE","m":"호수"},{"w":"PAGE","m":"쪽"},{"w":"SKY","m":"하늘"},{"w":"BRING","m":"가져오다"},{"w":"DISH","m":"접시"},{"w":"LAMP","m":"등불"},{"w":"PAINT","m":"칠하다"},{"w":"SLEEP","m":"잠자다"},{"w":"DOG","m":"개"},{"w":"GRASS","m":"풀"},{"w":"LAND","m":"땅"},{"w":"PAIR","m":"짝"},{"w":"SLIDE","m":"미끄러지다"},{"w":"BROWN","m":"갈색"},{"w":"DOCTOR","m":"의사"},{"w":"GRAY","m":"회색"},{"w":"LARGE","m":"큰"},{"w":"PANTS","m":"바지"},{"w":"SLOW","m":"느린"},{"w":"BRUSH","m":"솔"},{"w":"GREAT","m":"큰"},{"w":"LAST","m":"마지막"},{"w":"PAPER","m":"종이"},{"w":"SMALL","m":"작은"},{"w":"BUILD","m":"건설하다"},{"w":"DOLL","m":"인형"},{"w":"GREEN","m":"녹색"},{"w":"LATE","m":"늦은"},{"w":"SMELL","m":"냄새나다"},{"w":"BURN","m":"불타다"},{"w":"DOLLAR","m":"달러"},{"w":"GROUND","m":"땅"},{"w":"LAUGH","m":"웃다"},{"w":"PARK","m":"공원"},{"w":"SMILE","m":"웃다"},{"w":"BUS","m":"버스"},{"w":"DOLPHIN","m":"돌고래"},{"w":"GROUP","m":"단체"},{"w":"LEAD","m":"인도하다"},{"w":"SMOKE","m":"연기"},{"w":"BUSY","m":"바쁜"},{"w":"DOOR","m":"문"},{"w":"GROW","m":"성장하다"},{"w":"LEAF","m":"잎"},{"w":"PARTY","m":"파티"},{"w":"SNOW","m":"눈"},{"w":"DOWN","m":"아래에"},{"w":"LEARN","m":"배우다"},{"w":"PASS","m":"통과하다"},{"w":"DRAW","m":"그리다"},{"w":"LEAVE","m":"떠나다"},{"w":"PAY","m":"지불하다"},{"w":"SOAP","m":"비누"},{"w":"BUTTON","m":"단추"},{"w":"DREAM","m":"꿈"},{"w":"LEFT","m":"왼쪽"},{"w":"PEACE","m":"평화"},{"w":"SOCCER","m":"축구"},{"w":"BUY","m":"사다"},{"w":"DRESS","m":"드레스"},{"w":"LEG","m":"다리"},{"w":"PEAR","m":"배"},{"w":"SOCK","m":"양말"},{"w":"DRINK","m":"마시다"},{"w":"LESSON","m":"학과"},{"w":"PEN","m":"펜"},{"w":"SOFT","m":"부드러운"},{"w":"DRIVE","m":"운전하다"},{"w":"LET","m":"허락하다"},{"w":"PENCIL","m":"연필"},{"w":"SOME","m":"약간의"},{"w":"BYE","m":"안녕"},{"w":"DROP","m":"떨어지다"},{"w":"LETTER","m":"편지"},{"w":"PEOPLE","m":"사람"},{"w":"SON","m":"아들"},{"w":"DRUM","m":"북"},{"w":"LIBRARY","m":"도서관"},{"w":"PIANO","m":"피아노"},{"w":"SONG","m":"노래"},{"w":"DRY","m":"마른"},{"w":"LIGHT","m":"빛"},{"w":"PICK","m":"따다"},{"w":"SOON","m":"곧"},{"w":"DUCK","m":"오리"},{"w":"LIKE","m":"좋아하다"},{"w":"PICNIC","m":"소풍"},{"w":"SORRY","m":"미안한"},{"w":"LINE","m":"선"},{"w":"PICTURE","m":"그림"},{"w":"SOUND","m":"소리"},{"w":"LION","m":"사자"},{"w":"PIECE","m":"조각"},{"w":"SOUP","m":"스프"},{"w":"LIP","m":"입술"},{"w":"PIG","m":"돼지"},{"w":"SOUTH","m":"남쪽"},{"w":"LIST","m":"목록"},{"w":"PILOT","m":"조종사"},{"w":"SPACE","m":"공간"},{"w":"LISTEN","m":"듣다"},{"w":"PIN","m":"핀"},{"w":"SPEAK","m":"이야기하다"},{"w":"LITTLE","m":"작은"},{"w":"PINE","m":"소나무"},{"w":"SPEED","m":"속력"},{"w":"LIVE","m":"살다"},{"w":"PINK","m":"분홍"},{"w":"SPELL","m":"철자"},{"w":"LONG","m":"긴"},{"w":"PIPE","m":"파이프"},{"w":"LOOK","m":"바라보다"},{"w":"PLACE","m":"장소"},{"w":"SPOON","m":"숟가락"},{"w":"LOSE","m":"잃다"},{"w":"PLAN","m":"계획"},{"w":"SPORT","m":"운동경기"},{"w":"LOT","m":"많음"},{"w":"PLANE","m":"비행기"},{"w":"SPRING","m":"봄"},{"w":"LOVE","m":"사랑하다"},{"w":"PLANT","m":"식물"},{"w":"STAND","m":"서다"},{"w":"LOW","m":"낮은"},{"w":"PLAY","m":"놀다"},{"w":"STAR","m":"별"},{"w":"LUCK","m":"행운"},{"w":"PLEASE","m":"제발"},{"w":"START","m":"출발하다"},{"w":"LUNCH","m":"점심"},{"w":"POCKET","m":"주머니"},{"w":"STAY","m":"머물다"},{"w":"POLICE","m":"경찰"},{"w":"STEAM","m":"증기"},{"w":"POOL","m":"웅덩이"},{"w":"STEP","m":"한걸음"},{"w":"POOR","m":"가난한"},{"w":"STICK","m":"막대기"},{"w":"POST","m":"기둥"},{"w":"STOP","m":"멈추다"},{"w":"POSTER","m":"포스터"},{"w":"STORE","m":"가게"},{"w":"STORM","m":"폭풍우"},{"w":"PULL","m":"끌다"},{"w":"STORY","m":"이야기"},{"w":"PUSH","m":"밀다"},{"w":"PUT","m":"놓다"},{"w":"STREET","m":"거리"},{"w":"STRONG","m":"강한"},{"w":"STUDENT","m":"학생"},{"w":"STUDY","m":"공부하다"},{"w":"SUBWAY","m":"지하철"},{"w":"SUGAR","m":"설탕"},{"w":"SUMMER","m":"여름"},{"w":"SUN","m":"태양"},{"w":"SUPPER","m":"저녁식사"},{"w":"SURE","m":"확실한"},{"w":"SWEET","m":"달콤한"},{"w":"SWIM","m":"수영"},{"w":"SWING","m":"흔들리다"},{"w":"SWITCH","m":"스위치"},{"w":"VACATION","m":"휴가"},{"w":"VILLAGE","m":"마을"}];

function shuffle(a){for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]];}return a;}

function generatePuzzle(){
  const pool=shuffle([...POOL]).filter(x=>x.w.length>=3&&x.w.length<=7);
  const TRIES=300,TARGET=7,GMAX=12;
  let best=null,bestScore=0;
  for(let t=0;t<TRIES;t++){
    const words=shuffle([...pool]).slice(0,50);
    const result=tryBuild(words,TARGET,GMAX);
    if(result&&result.placed.length>bestScore){best=result;bestScore=result.placed.length;if(bestScore>=TARGET)break;}
  }
  return best;
}

function tryBuild(words,target,GMAX){
  const placed=[];
  const grid=Array.from({length:GMAX},()=>Array(GMAX).fill(''));
  const OFF=Math.floor(GMAX/2);
  function fits(word,r,c,dir){
    if(dir==='across'){if(c<0||c+word.length>GMAX)return false;if(c>0&&grid[r][c-1])return false;if(c+word.length<GMAX&&grid[r][c+word.length])return false;}
    else{if(r<0||r+word.length>GMAX)return false;if(r>0&&grid[r-1][c])return false;if(r+word.length<GMAX&&grid[r+word.length][c])return false;}
    let intersects=0;
    for(let i=0;i<word.length;i++){
      const cr=dir==='down'?r+i:r,cc=dir==='across'?c+i:c;
      const existing=grid[cr][cc];
      if(existing){if(existing!==word[i])return false;intersects++;}
      else{
        if(dir==='across'){if(cr>0&&grid[cr-1][cc])return false;if(cr<GMAX-1&&grid[cr+1][cc])return false;}
        else{if(cc>0&&grid[cr][cc-1])return false;if(cc<GMAX-1&&grid[cr][cc+1])return false;}
      }
    }
    if(placed.length>0&&intersects===0)return false;
    return true;
  }
  function place(word,r,c,dir){for(let i=0;i<word.length;i++){const cr=dir==='down'?r+i:r,cc=dir==='across'?c+i:c;grid[cr][cc]=word[i];}}
  const first=words[0];
  const fr=OFF,fc=OFF-Math.floor(first.w.length/2);
  place(first.w,fr,fc,'across');
  placed.push({word:first.w,m:first.m,r:fr,c:fc,dir:'across'});
  for(let wi=1;wi<words.length&&placed.length<target;wi++){
    const entry=words[wi];
    let found=false;
    const dirs=Math.random()<0.5?['across','down']:['down','across'];
    for(const dir of dirs){
      if(found)break;
      for(let pi=0;pi<placed.length&&!found;pi++){
        const p=placed[pi];
        for(let i=0;i<entry.w.length&&!found;i++){
          const ch=entry.w[i];
          for(let j=0;j<p.word.length&&!found;j++){
            if(p.word[j]===ch){
              let r,c;
              if(dir==='across'&&p.dir==='down'){r=p.r+j;c=p.c-i;}
              else if(dir==='down'&&p.dir==='across'){r=p.r-i;c=p.c+j;}
              else continue;
              if(fits(entry.w,r,c,dir)){place(entry.w,r,c,dir);placed.push({word:entry.w,m:entry.m,r,c,dir});found=true;}
            }
          }
        }
      }
    }
  }
  if(placed.length<4)return null;
  let minR=GMAX,minC=GMAX,maxR=0,maxC=0;
  placed.forEach(p=>{
    minR=Math.min(minR,p.r);minC=Math.min(minC,p.c);
    const er=p.dir==='down'?p.r+p.word.length-1:p.r;
    const ec=p.dir==='across'?p.c+p.word.length-1:p.c;
    maxR=Math.max(maxR,er);maxC=Math.max(maxC,ec);
  });
  const normalized=placed.map(p=>({...p,r:p.r-minR,c:p.c-minC}));
  return{placed:normalized,rows:maxR-minR+1,cols:maxC-minC+1};
}

let puzzle,grid,SIZE,cells,activeR,activeC,activeDir,wordDefs;

function buildGrid(placed,rows,cols){
  const g=Array.from({length:rows},()=>Array.from({length:cols},()=>({answer:'',num:0,across:-1,down:-1})));
  placed.forEach((p,wi)=>{
    for(let i=0;i<p.word.length;i++){
      const r=p.r+(p.dir==='down'?i:0),c=p.c+(p.dir==='across'?i:0);
      g[r][c].answer=p.word[i];
      if(p.dir==='across')g[r][c].across=wi;else g[r][c].down=wi;
    }
  });
  let num=1;const nm={};
  placed.forEach((p)=>{
    const key=p.r+','+p.c;
    if(!nm[key]){nm[key]=num++;g[p.r][p.c].num=nm[key];}
    p.num=nm[key];
  });
  return g;
}

function initPuzzle(){
  const gen=generatePuzzle();
  if(!gen){setTimeout(initPuzzle,50);return;}
  puzzle=gen.placed;SIZE={rows:gen.rows,cols:gen.cols};
  grid=buildGrid(puzzle,SIZE.rows,SIZE.cols);
  cells={};activeR=null;activeC=null;activeDir='across';
  wordDefs={across:[],down:[]};
  puzzle.forEach((p,i)=>{p.idx=i;if(p.dir==='across')wordDefs.across.push(p);else wordDefs.down.push(p);});
  wordDefs.across.sort((a,b)=>a.num-b.num);
  wordDefs.down.sort((a,b)=>a.num-b.num);
  renderGrid();renderClues();setMsg('','');updateProg();
}

function renderGrid(){
  const el=document.getElementById('cw-grid');
  el.style.gridTemplateColumns=`repeat(${SIZE.cols},48px)`;
  el.style.gridTemplateRows=`repeat(${SIZE.rows},48px)`;
  el.innerHTML='';
  for(let r=0;r<SIZE.rows;r++){
    for(let c=0;c<SIZE.cols;c++){
      const cell=grid[r][c];
      const div=document.createElement('div');
      div.className='cw-cell'+(cell.answer?'':' blocked');
      div.dataset.r=r;div.dataset.c=c;
      cells[r+','+c]=div;
      if(cell.answer){
        if(cell.num){const sp=document.createElement('span');sp.className='cw-num';sp.textContent=cell.num;div.appendChild(sp);}
        const inp=document.createElement('input');
        inp.maxLength=1;inp.autocomplete='off';inp.setAttribute('autocorrect','off');inp.setAttribute('autocapitalize','characters');inp.spellcheck=false;
        inp.dataset.r=r;inp.dataset.c=c;
        inp.addEventListener('click',onCellClick);
        inp.addEventListener('keydown',onKey);
        inp.addEventListener('input',onInput);
        div.appendChild(inp);
      }
      el.appendChild(div);
    }
  }
}

function getInput(r,c){const d=cells[r+','+c];return d?d.querySelector('input'):null;}

function highlightWord(){
  for(let r=0;r<SIZE.rows;r++)for(let c=0;c<SIZE.cols;c++){
    const d=cells[r+','+c];
    if(d&&!d.classList.contains('blocked')&&!d.classList.contains('correct')&&!d.classList.contains('wrong'))
      d.classList.remove('highlight','active');
  }
  if(activeR===null)return;
  const cell=grid[activeR][activeC];
  const wIdx=activeDir==='across'?cell.across:cell.down;
  if(wIdx<0)return;
  const p=puzzle[wIdx];
  for(let i=0;i<p.word.length;i++){
    const r=p.r+(p.dir==='down'?i:0),c=p.c+(p.dir==='across'?i:0);
    const d=cells[r+','+c];if(d)d.classList.add('highlight');
  }
  const act=cells[activeR+','+activeC];
  if(act){act.classList.remove('highlight');act.classList.add('active');}
  updateClueHL();
}

function updateClueHL(){
  document.querySelectorAll('.clue-item').forEach(el=>el.classList.remove('active-clue'));
  if(activeR===null)return;
  const cell=grid[activeR][activeC];
  const wIdx=activeDir==='across'?cell.across:cell.down;
  if(wIdx<0)return;
  const el=document.getElementById('clue-'+wIdx);
  if(el){el.classList.add('active-clue');el.scrollIntoView({block:'nearest'});}
}

function onCellClick(e){
  const r=parseInt(e.target.dataset.r),c=parseInt(e.target.dataset.c);
  const cell=grid[r][c];
  if(r===activeR&&c===activeC){
    activeDir=activeDir==='across'?'down':'across';
    const hasDir=activeDir==='across'?cell.across>=0:cell.down>=0;
    if(!hasDir)activeDir=activeDir==='across'?'down':'across';
  }else{
    activeR=r;activeC=c;
    const ha=cell.across>=0,hd=cell.down>=0;
    if(!ha&&hd)activeDir='down';else if(ha&&!hd)activeDir='across';
  }
  updateDirBtns();highlightWord();e.target.focus();
}

function onInput(e){
  const inp=e.target;
  const val=inp.value.toUpperCase().replace(/[^A-Z]/g,'');
  inp.value=val?val[val.length-1]:'';
  if(inp.value)moveNext();updateProg();
}

function onKey(e){
  const r=parseInt(e.target.dataset.r),c=parseInt(e.target.dataset.c);
  if(e.key==='Backspace'&&!e.target.value){movePrev(r,c);e.preventDefault();}
  if(e.key==='ArrowRight'){activeDir='across';highlightWord();moveNext();e.preventDefault();}
  if(e.key==='ArrowLeft'){activeDir='across';highlightWord();movePrev(r,c);e.preventDefault();}
  if(e.key==='ArrowDown'){activeDir='down';highlightWord();moveNext();e.preventDefault();}
  if(e.key==='ArrowUp'){activeDir='down';highlightWord();movePrev(r,c);e.preventDefault();}
}

function moveNext(){
  if(activeR===null)return;
  let r=activeR,c=activeC;
  while(true){
    if(activeDir==='across')c++;else r++;
    if(r<0||r>=SIZE.rows||c<0||c>=SIZE.cols)break;
    if(grid[r][c].answer){activeR=r;activeC=c;break;}
  }
  highlightWord();const inp=getInput(activeR,activeC);if(inp)inp.focus();
}

function movePrev(fr,fc){
  let r=fr,c=fc;
  while(true){
    if(activeDir==='across')c--;else r--;
    if(r<0||r>=SIZE.rows||c<0||c>=SIZE.cols)break;
    if(grid[r][c].answer){activeR=r;activeC=c;break;}
  }
  highlightWord();const inp=getInput(activeR,activeC);if(inp)inp.focus();
}

function renderClues(){
  ['across','down'].forEach(dir=>{
    const el=document.getElementById('clues-'+dir);el.innerHTML='';
    wordDefs[dir].forEach(p=>{
      const d=document.createElement('div');
      d.className='clue-item';d.id='clue-'+p.idx;
      d.innerHTML=`<span class="clue-num">${p.num}.</span><span>${p.word.length} letters &nbsp;<span class="clue-ko">— ${p.m}</span></span>`;
      d.addEventListener('click',()=>{
        activeR=p.r;activeC=p.c;activeDir=p.dir;
        updateDirBtns();highlightWord();
        const inp=getInput(activeR,activeC);if(inp)inp.focus();
      });
      el.appendChild(d);
    });
  });
}

function checkAll(){
  let allFilled=true,allRight=true;
  for(let r=0;r<SIZE.rows;r++)for(let c=0;c<SIZE.cols;c++){
    const cell=grid[r][c];if(!cell.answer)continue;
    const inp=getInput(r,c);if(!inp)continue;
    const v=inp.value.toUpperCase();
    const d=cells[r+','+c];
    d.classList.remove('correct','wrong');
    if(!v)allFilled=false;
    else if(v===cell.answer)d.classList.add('correct');
    else{d.classList.add('wrong');allRight=false;}
  }
  if(allFilled&&allRight)setMsg('🎉 Amazing! You solved it!','success');
  else if(!allFilled)setMsg('Fill all the squares first!','info');
  else setMsg('Some answers are wrong. Try again!','error');
}

function revealAll(){
  for(let r=0;r<SIZE.rows;r++)for(let c=0;c<SIZE.cols;c++){
    const cell=grid[r][c];if(!cell.answer)continue;
    const inp=getInput(r,c);if(inp)inp.value=cell.answer;
    const d=cells[r+','+c];d.classList.remove('wrong');d.classList.add('correct');
  }
  setMsg('Here are all the answers!','info');updateProg();
}

function setMsg(text,cls){const el=document.getElementById('cw-msg');el.textContent=text;el.className=cls;}

function updateProg(){
  let filled=0,total=0;
  for(let r=0;r<SIZE.rows;r++)for(let c=0;c<SIZE.cols;c++){
    if(grid[r][c].answer){total++;const inp=getInput(r,c);if(inp&&inp.value)filled++;}
  }
  document.getElementById('cw-prog').textContent=filled+'/'+total+' letters filled';
  puzzle.forEach((p,wi)=>{
    let done=true;
    for(let i=0;i<p.word.length;i++){
      const r=p.r+(p.dir==='down'?i:0),c=p.c+(p.dir==='across'?i:0);
      const inp=getInput(r,c);
      if(!inp||inp.value.toUpperCase()!==p.word[i]){done=false;break;}
    }
    const el=document.getElementById('clue-'+wi);
    if(el){if(done)el.classList.add('done-clue');else el.classList.remove('done-clue');}
  });
}

function updateDirBtns(){
  document.getElementById('btn-across').classList.toggle('on',activeDir==='across');
  document.getElementById('btn-down').classList.toggle('on',activeDir==='down');
}

document.getElementById('btn-check').onclick=checkAll;
document.getElementById('btn-reveal').onclick=revealAll;
document.getElementById('btn-new').onclick=initPuzzle;
document.getElementById('btn-across').onclick=()=>{activeDir='across';updateDirBtns();highlightWord();}
document.getElementById('btn-down').onclick=()=>{activeDir='down';updateDirBtns();highlightWord();}

initPuzzle();
</script>
</body>
</html>
