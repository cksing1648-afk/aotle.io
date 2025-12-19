import React, { useState, useMemo } from 'react';
import { Dialog } from '@headlessui/react';
import { X, Share2, ChevronUp, ChevronDown } from 'lucide-react';
import { motion } from 'framer-motion';

// --- 步驟一：整合並格式化您的 Excel 資料 ---
// 我已將您提供的 CSV 資料轉換為 JavaScript 物件陣列。
// 多重屬性（如 "中央, 憲兵"）已被處理成陣列（如 ['中央', '憲兵']）。
const characterData = [
  { name: "拉爾夫", gender: "男", affiliation: ["中央", "憲兵"], attribute: ["艾爾迪亞"], firstAppearance: 5 },
  { name: "肯尼·阿卡曼", gender: "男", affiliation: ["中央", "憲兵"], attribute: ["艾爾迪亞", "阿卡曼"], firstAppearance: 5 },
  { name: "特勞特・卡芬", gender: "女", affiliation: ["中央", "憲兵"], attribute: ["艾爾迪亞"], firstAppearance: 5 },
  { name: "都蘭", gender: "男", affiliation: ["中央", "憲兵"], attribute: ["艾爾迪亞"], firstAppearance: 5 },
  { name: "傑爾・薩內斯", gender: "男", affiliation: ["中央", "憲兵"], attribute: ["艾爾迪亞"], firstAppearance: 5 },
  { name: "達里斯·薩克雷", gender: "男", affiliation: ["王政府"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "芙莉妲·雷斯", gender: "女", affiliation: ["王政府", "城牆教"], attribute: ["艾爾迪亞", "王族", "巨人"], firstAppearance: 5 },
  { name: "烏利·雷斯", gender: "男", affiliation: ["王政府", "城牆教"], attribute: ["艾爾迪亞", "王族", "巨人"], firstAppearance: 5 },
  { name: "羅德·雷斯", gender: "男", affiliation: ["王政府", "城牆教"], attribute: ["艾爾迪亞", "王族", "巨人"], firstAppearance: 5 },
  { name: "卡露拉·葉卡", gender: "女", affiliation: ["帕拉迪島"], attribute: ["艾爾迪亞"], firstAppearance: 1 },
  { name: "迪墨·利布斯", gender: "男", affiliation: ["帕拉迪島"], attribute: ["艾爾迪亞"], firstAppearance: 1 },
  { name: "索尼", gender: "未知", affiliation: ["帕拉迪島"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 2 },
  { name: "賓", gender: "未知", affiliation: ["帕拉迪島"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 2 },
  { name: "弗雷格爾·利布斯", gender: "男", affiliation: ["帕拉迪島"], attribute: ["艾爾迪亞"], firstAppearance: 5 },
  { name: "庫契爾·阿卡曼", gender: "女", affiliation: ["帕拉迪島"], attribute: ["艾爾迪亞", "阿卡曼"], firstAppearance: 5 },
  { name: "畢雷", gender: "男", affiliation: ["帕拉迪島"], attribute: ["艾爾迪亞"], firstAppearance: 5 },
  { name: "路易潔", gender: "女", affiliation: ["帕拉迪島", "葉卡"], attribute: ["艾爾迪亞"], firstAppearance: 1 },
  { name: "史爾瑪", gender: "男", affiliation: ["帕拉迪島", "葉卡"], attribute: ["艾爾迪亞"], firstAppearance: 8 },
  { name: "古利夏·葉卡", gender: "男", affiliation: ["帕拉迪島", "瑪雷", "反抗軍"], attribute: ["艾爾迪亞", "牆外", "巨人"], firstAppearance: 1 },
  { name: "葛利茲", gender: "男", affiliation: ["帕拉迪島", "瑪雷", "葉卡"], attribute: ["瑪雷"], firstAppearance: 8 },
  { name: "尼克神父", gender: "男", affiliation: ["城牆教"], attribute: ["艾爾迪亞"], firstAppearance: 1 },
  { name: "托馬斯·瓦格納", gender: "男", affiliation: ["第104期"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "米力伍斯·賽姆斯基", gender: "男", affiliation: ["第104期"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "米娜·卡羅萊納", gender: "女", affiliation: ["第104期"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "奈克·提亞斯", gender: "男", affiliation: ["第104期"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "法蘭茲·克夫卡", gender: "男", affiliation: ["第104期"], attribute: ["艾爾迪亞", "笨蛋夫妻"], firstAppearance: 2 },
  { name: "馬可·波特", gender: "男", affiliation: ["第104期"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "漢娜·迪亞曼多", gender: "女", affiliation: ["第104期"], attribute: ["艾爾迪亞", "笨蛋夫妻"], firstAppearance: 2 },
  { name: "山姆耶爾·林克-傑克遜", gender: "男", affiliation: ["第104期", "葉卡"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "達茲", gender: "男", affiliation: ["第104期", "葉卡"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "米卡莎·阿卡曼", gender: "女", affiliation: ["第104期", "調查"], attribute: ["艾爾迪亞", "阿卡曼"], firstAppearance: 1 },
  { name: "阿爾敏·亞魯雷特", gender: "男", affiliation: ["第104期", "調查"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 1 },
  { name: "柯尼·史普林格", gender: "男", affiliation: ["第104期", "調查"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "約翰·基爾休坦", gender: "男", affiliation: ["第104期", "調查"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "莎夏·布勞斯", gender: "女", affiliation: ["第104期", "調查"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "希斯特莉亞·雷斯", gender: "女", affiliation: ["第104期", "調查", "王政府"], attribute: ["艾爾迪亞", "王族"], firstAppearance: 2 },
  { name: "艾連·葉卡", gender: "男", affiliation: ["第104期", "調查", "葉卡"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 1 },
  { name: "尤米爾", gender: "女", affiliation: ["第104期", "調查", "瑪雷"], attribute: ["艾爾迪亞", "巨人", "瑪雷"], firstAppearance: 2 },
  { name: "貝爾托特·胡佛", gender: "男", affiliation: ["第104期", "調查", "戰士隊"], attribute: ["艾爾迪亞", "牆外", "巨人"], firstAppearance: 2 },
  { name: "亞妮·雷恩哈特", gender: "女", affiliation: ["第104期", "調查", "戰士隊"], attribute: ["艾爾迪亞", "牆外", "巨人"], firstAppearance: 2 },
  { name: "萊納·布朗", gender: "男", affiliation: ["第104期", "調查", "戰士隊"], attribute: ["艾爾迪亞", "牆外", "巨人"], firstAppearance: 2 },
  { name: "珊德拉", gender: "女", affiliation: ["第104期", "駐紮", "調查"], attribute: ["艾爾迪亞"], firstAppearance: 6 },
  { name: "哥頓", gender: "男", affiliation: ["第104期", "駐紮", "調查"], attribute: ["艾爾迪亞"], firstAppearance: 6 },
  { name: "弗洛克·福斯特", gender: "男", affiliation: ["第104期", "駐紮", "調查", "葉卡"], attribute: ["艾爾迪亞"], firstAppearance: 6 },
  { name: "菲·葉卡", gender: "女", affiliation: ["瑪雷"], attribute: ["艾爾迪亞"], firstAppearance: 6 },
  { name: "卡爾畢", gender: "男", affiliation: ["瑪雷"], attribute: ["瑪雷"], firstAppearance: 7 },
  { name: "威利·戴巴", gender: "男", affiliation: ["瑪雷"], attribute: ["瑪雷"], firstAppearance: 7 },
  { name: "迪奧·馬迦特", gender: "男", affiliation: ["瑪雷"], attribute: ["瑪雷"], firstAppearance: 7 },
  { name: "黛娜·葉卡", gender: "女", affiliation: ["瑪雷", "反抗軍"], attribute: ["牆外", "王族", "巨人", "艾爾迪亞"], firstAppearance: 1 },
  { name: "艾連·克魯格", gender: "男", affiliation: ["瑪雷", "反抗軍", "治安局"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 6 },
  { name: "伊雷娜", gender: "女", affiliation: ["瑪雷", "吉克"], attribute: ["瑪雷"], firstAppearance: 8 },
  { name: "尼柯洛", gender: "男", affiliation: ["瑪雷", "帕拉迪島"], attribute: ["瑪雷"], firstAppearance: 7 },
  { name: "古洛斯", gender: "男", affiliation: ["瑪雷", "治安局"], attribute: ["艾爾迪亞"], firstAppearance: 6 },
  { name: "艾爾文·史密斯", gender: "男", affiliation: ["調查"], attribute: ["艾爾迪亞"], firstAppearance: 1 },
  { name: "迪塔·涅斯", gender: "男", affiliation: ["調查"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "克拉斯", gender: "男", affiliation: ["調查"], attribute: ["艾爾迪亞"], firstAppearance: 6 },
  { name: "迪爾克", gender: "男", affiliation: ["調查"], attribute: ["艾爾迪亞"], firstAppearance: 6 },
  { name: "馬雷涅", gender: "女", affiliation: ["調查"], attribute: ["艾爾迪亞"], firstAppearance: 6 },
  { name: "吉爾迦", gender: "男", affiliation: ["調查", "米可"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "托瑪", gender: "男", affiliation: ["調查", "米可"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "米可·薩卡利亞斯", gender: "男", affiliation: ["調查", "米可"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "納拿巴", gender: "女", affiliation: ["調查", "米可"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "賀寧格", gender: "男", affiliation: ["調查", "米可"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "麗奈", gender: "女", affiliation: ["調查", "米可"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "艾魯多·琴", gender: "男", affiliation: ["調查", "里維"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "里維·阿卡曼", gender: "男", affiliation: ["調查", "里維"], attribute: ["艾爾迪亞", "阿卡曼"], firstAppearance: 3 },
  { name: "佩托拉·拉爾", gender: "女", affiliation: ["調查", "里維"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "格達·修茲", gender: "男", affiliation: ["調查", "里維"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "歐魯·波札德", gender: "男", affiliation: ["調查", "里維"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "巴利斯", gender: "男", affiliation: ["調查", "里維"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 8 },
  { name: "基斯·沙迪斯", gender: "男", affiliation: ["調查", "訓練"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "阿貝爾", gender: "男", affiliation: ["調查", "漢吉"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "莫布里特·柏納", gender: "男", affiliation: ["調查", "漢吉"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "凱吉", gender: "男", affiliation: ["調查", "漢吉"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "漢吉·佐耶", gender: "未知", affiliation: ["調查", "漢吉"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "妮法", gender: "女", affiliation: ["調查", "漢吉"], attribute: ["艾爾迪亞"], firstAppearance: 4 },
  { name: "拉沙德", gender: "男", affiliation: ["調查", "漢吉"], attribute: ["艾爾迪亞"], firstAppearance: 4 },
  { name: "勞達", gender: "男", affiliation: ["調查", "漢吉"], attribute: ["艾爾迪亞"], firstAppearance: 4 },
  { name: "漢尼斯", gender: "男", affiliation: ["駐紮"], attribute: ["艾爾迪亞"], firstAppearance: 1 },
  { name: "古斯塔夫", gender: "男", affiliation: ["駐紮"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "伊安·迪特里西", gender: "男", affiliation: ["駐紮"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "卡斯特", gender: "男", affiliation: ["駐紮"], attribute: ["艾爾迪亞"], firstAppearance: 5 },
  { name: "安卡·萊恩貝爾加", gender: "女", affiliation: ["駐紮"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "米塔比·雅哈", gender: "男", affiliation: ["駐紮"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "里柯·布雷琴斯卡", gender: "女", affiliation: ["駐紮"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "基茨·威爾曼", gender: "男", affiliation: ["駐紮"], attribute: ["艾爾迪亞"], firstAppearance: 2 },
  { name: "達特·皮克希斯", gender: "男", affiliation: ["駐紮"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 2 },
  { name: "洛柏夫", gender: "男", affiliation: ["駐紮", "調查"], attribute: ["艾爾迪亞"], firstAppearance: 8 },
  { name: "希琪", gender: "女", affiliation: ["憲兵"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "奈爾·德克", gender: "男", affiliation: ["憲兵"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "霍爾茲", gender: "男", affiliation: ["憲兵"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "馬爾洛", gender: "男", affiliation: ["憲兵", "調查"], attribute: ["艾爾迪亞"], firstAppearance: 3 },
  { name: "吉克·葉卡", gender: "男", affiliation: ["戰士隊"], attribute: ["艾爾迪亞", "牆外", "王族", "巨人"], firstAppearance: 3 },
  { name: "馬賽爾‧賈利亞德", gender: "男", affiliation: ["戰士隊"], attribute: ["艾爾迪亞", "牆外", "巨人"], firstAppearance: 4 },
  { name: "皮克", gender: "女", affiliation: ["戰士隊"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 6 },
  { name: "卡爾洛", gender: "男", affiliation: ["戰士隊"], attribute: ["艾爾迪亞"], firstAppearance: 7 },
  { name: "法爾可‧葛萊斯", gender: "男", affiliation: ["戰士隊"], attribute: ["艾爾迪亞"], firstAppearance: 7 },
  { name: "波爾柯‧賈利亞德", gender: "男", affiliation: ["戰士隊"], attribute: ["艾爾迪亞", "巨人"], firstAppearance: 7 },
  { name: "柯特‧葛萊斯", gender: "男", affiliation: ["戰士隊"], attribute: ["艾爾迪亞"], firstAppearance: 7 },
  { name: "烏德", gender: "男", affiliation: ["戰士隊"], attribute: ["艾爾迪亞"], firstAppearance: 7 },
  { name: "索菲亞", gender: "女", affiliation: ["戰士隊"], attribute: ["艾爾迪亞"], firstAppearance: 7 },
  { name: "賈碧‧布朗", gender: "女", affiliation: ["戰士隊"], attribute: ["艾爾迪亞"], firstAppearance: 7 },
];

const MAX_GUESSES = 8;
const ATTRIBUTES_TO_COMPARE = ['gender', 'affiliation', 'attribute', 'firstAppearance'];

const getDailySolution = () => {
  const epoch = new Date('2025-12-19');
  const today = new Date();
  today.setHours(0, 0, 0, 0);
  const index = Math.floor((today - epoch) / (1000 * 60 * 60 * 24));
  return characterData[index % characterData.length];
};

const attributeLabels = {
  name: '角色',
  gender: '性別',
  affiliation: '陣營',
  attribute: '特徵',
  firstAppearance: '初登場篇章',
};

// --- 主元件 ---
export default function AotAttributeWordleAdvanced() {
  const solution = useMemo(() => getDailySolution(), []);
  const [guesses, setGuesses] = useState([]);
  const [currentGuessName, setCurrentGuessName] = useState('');
  const [isGameOver, setIsGameOver] = useState(false);
  const [gameStatus, setGameStatus] = useState('PLAYING');
  const [isModalOpen, setIsModalOpen] = useState(false);
  const [searchTerm, setSearchTerm] = useState('');

  const characterNames = useMemo(() => characterData.map(c => c.name), []);
  const alreadyGuessedNames = useMemo(() => guesses.map(g => g.name), [guesses]);

  const filteredCharacters = useMemo(() => {
    if (!searchTerm) return [];
    return characterNames.filter(name => 
      name.includes(searchTerm) && !alreadyGuessedNames.includes(name)
    ).slice(0, 5);
  }, [searchTerm, characterNames, alreadyGuessedNames]);

  const handleSelectCharacter = (name) => {
    setCurrentGuessName(name);
    setSearchTerm('');
  };

  const handleSubmitGuess = () => {
    if (!currentGuessName || guesses.length >= MAX_GUESSES) return;
    const guessObject = characterData.find(c => c.name === currentGuessName);
    if (!guessObject) return;

    const newGuesses = [...guesses, guessObject];
    setGuesses(newGuesses);
    setCurrentGuessName('');

    if (guessObject.name === solution.name) {
      setGameStatus('WON');
      setIsGameOver(true);
      setTimeout(() => setIsModalOpen(true), 1600);
    } else if (newGuesses.length === MAX_GUESSES) {
      setGameStatus('LOST');
      setIsGameOver(true);
      setTimeout(() => setIsModalOpen(true), 1600);
    }
  };

  const getFeedback = (guess, solution, attribute) => {
    const guessValue = guess[attribute];
    const solutionValue = solution[attribute];

    if (attribute === 'firstAppearance') {
      if (guessValue === solutionValue) return 'correct';
      return guessValue < solutionValue ? 'higher' : 'lower';
    }

    if (Array.isArray(guessValue) && Array.isArray(solutionValue)) {
      const sortedGuess = [...guessValue].sort().join(',');
      const sortedSolution = [...solutionValue].sort().join(',');
      if (sortedGuess === sortedSolution) return 'correct';
      
      const hasIntersection = guessValue.some(val => solutionValue.includes(val));
      if (hasIntersection) return 'partial';
      
      return 'incorrect';
    }

    return guessValue === solutionValue ? 'correct' : 'incorrect';
  };
  
  const shareResult = () => {
    const dayIndex = Math.floor((new Date() - new Date('2025-12-19')) / (1000 * 60 * 60 * 24));
    const title = `巨人推理 #${dayIndex}`;
    const resultGrid = guesses
      .map(guess =>
        ATTRIBUTES_TO_COMPARE.map(attr => {
          const feedback = getFeedback(guess, solution, attr);
          if (feedback === 'correct') return '🟩';
          if (feedback === 'partial') return '🟨';
          if (feedback === 'higher') return '🔼';
          if (feedback === 'lower') return '🔽';
          return '🟥';
        }).join('')
      )
      .join('\n');
    const text = `${title} (${guesses.length}/${MAX_GUESSES})\n\n${resultGrid}\n\n你能猜出是誰嗎？`;
    navigator.clipboard.writeText(text).then(() => {
      alert('結果已複製到剪貼簿！');
    });
  };

  const FeedbackCell = ({ guess, solution, attribute, index }) => {
    const feedback = getFeedback(guess, solution, attribute);
    const value = guess[attribute];
    
    let bgColor = 'bg-red-800/80';
    if (feedback === 'correct') bgColor = 'bg-green-600/80';
    if (feedback === 'partial') bgColor = 'bg-yellow-500/80';

    const content = Array.isArray(value) ? value.join(', ') : value;

    return (
      <motion.div
        className={`h-full w-full flex items-center justify-center rounded-md text-white font-bold text-xs sm:text-sm p-2 text-center ${bgColor}`}
        initial={{ opacity: 0, scale: 0.8, rotateY: 180 }}
        animate={{ opacity: 1, scale: 1, rotateY: 0 }}
        transition={{ delay: index * 0.15, duration: 0.5 }}
      >
        <div className="flex items-center gap-1">
          <span>{content}</span>
          {attribute === 'firstAppearance' && feedback === 'higher' && <ChevronUp size={16} />}
          {attribute === 'firstAppearance' && feedback === 'lower' && <ChevronDown size={16} />}
        </div>
      </motion.div>
    );
  };

  return (
    <div className="bg-gray-900 text-gray-100 min-h-screen flex flex-col items-center pt-6 pb-4 px-2 font-sans">
      <header className="mb-4 text-center">
        <h1 className="text-3xl sm:text-4xl font-bold tracking-wider uppercase text-white">巨人推理</h1>
        <p className="text-gray-400 mt-1">根據性別、陣營、特徵、登場篇章猜出角色</p>
      </header>
      
      <div className="w-full max-w-2xl flex flex-col items-center gap-3 mb-4">
        <div className="relative w-full max-w-md">
          <input
            type="text"
            value={searchTerm}
            onChange={(e) => setSearchTerm(e.target.value)}
            placeholder="輸入角色名稱搜尋..."
            className="w-full p-3 bg-gray-800 border-2 border-gray-600 rounded-lg focus:outline-none focus:border-blue-500 transition-colors"
            disabled={isGameOver}
          />
          {filteredCharacters.length > 0 && (
            <div className="absolute top-full left-0 right-0 mt-1 bg-gray-800 border border-gray-600 rounded-lg z-10 max-h-60 overflow-y-auto">
              {filteredCharacters.map(name => (
                <div
                  key={name}
                  onClick={() => handleSelectCharacter(name)}
                  className="p-3 hover:bg-gray-700 cursor-pointer"
                >
                  {name}
                </div>
              ))}
            </div>
          )}
        </div>
        <div className="flex items-center gap-4 w-full max-w-md">
            <div className="flex-grow h-12 flex items-center justify-center bg-gray-700 rounded-lg text-lg font-semibold px-2 truncate">
                {currentGuessName || '已選擇的角色'}
            </div>
            <button
                onClick={handleSubmitGuess}
                disabled={!currentGuessName || isGameOver}
                className="px-6 py-3 bg-green-600 text-white font-bold rounded-lg hover:bg-green-700 disabled:bg-gray-500 disabled:cursor-not-allowed transition-colors"
            >
                猜測
            </button>
        </div>
      </div>

      <div className="w-full max-w-4xl px-2">
        <div className="grid grid-cols-5 gap-1 sm:gap-2 text-center font-bold mb-2 text-xs sm:text-sm">
          <div className="bg-gray-700/50 rounded-md py-2">{attributeLabels.name}</div>
          {ATTRIBUTES_TO_COMPARE.map(attr => <div key={attr} className="bg-gray-700/50 rounded-md py-2">{attributeLabels[attr]}</div>)}
        </div>
        
        <div className="flex flex-col gap-1 sm:gap-2">
          {guesses.map((guess, guessIndex) => (
            <motion.div 
              key={guessIndex} 
              className="grid grid-cols-5 gap-1 sm:gap-2 h-16 sm:h-20"
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              transition={{ duration: 0.3 }}
            >
              <div className="bg-gray-800 rounded-md flex items-center justify-center text-center font-semibold p-1 text-sm sm:text-base">{guess.name}</div>
              {ATTRIBUTES_TO_COMPARE.map((attr, attrIndex) => (
                <FeedbackCell key={attr} guess={guess} solution={solution} attribute={attr} index={attrIndex} />
              ))}
            </motion.div>
          ))}
          {Array(MAX_GUESSES - guesses.length).fill(0).map((_, i) => (
             <div key={i} className="grid grid-cols-5 gap-1 sm:gap-2 h-16 sm:h-20">
                <div className="bg-gray-800/30 rounded-md"></div>
                {ATTRIBUTES_TO_COMPARE.map(attr => <div key={attr} className="bg-gray-800/30 rounded-md"></div>)}
             </div>
          ))}
        </div>
      </div>

      <Dialog open={isModalOpen} onClose={() => setIsModalOpen(false)} className="relative z-50">
        <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ duration: 0.3 }} className="fixed inset-0 bg-black/70" aria-hidden="true" />
        <div className="fixed inset-0 flex items-center justify-center p-4">
          <Dialog.Panel as={motion.div} initial={{ scale: 0.9, opacity: 0 }} animate={{ scale: 1, opacity: 1 }} className="w-full max-w-sm rounded-xl bg-gray-800 p-6 text-center shadow-2xl">
            <Dialog.Title className="text-2xl font-bold mb-2 text-white">
              {gameStatus === 'WON' ? '恭喜你，猜對了！' : '可惜，次數用完了'}
            </Dialog.Title>
            <p className="mb-4 text-lg text-gray-300">今天的答案是：<span className="font-bold text-green-400">{solution.name}</span></p>
            <div className="flex flex-col items-center gap-4">
              <button onClick={shareResult} className="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-4 rounded-lg flex items-center justify-center gap-2 transition-colors">
                <Share2 size={20} /> 分享你的結果
              </button>
              <button onClick={() => setIsModalOpen(false)} className="w-full bg-gray-600 hover:bg-gray-700 text-white font-bold py-3 px-4 rounded-lg flex items-center justify-center gap-2 transition-colors">
                <X size={20} /> 關閉
              </button>
            </div>
          </Dialog.Panel>
        </div>
      </Dialog>
    </div>
  );
}
