import React, { useState } from "react";

const questions = [
  {
    question: "데이트에서 가장 중요한 것은?",
    options: ["재미", "안정감", "설렘", "편안함"],
  },
  {
    question: "연락 스타일은?",
    options: ["자주 한다", "필요할 때만", "감정 따라", "규칙적"],
  },
  {
    question: "갈등이 생기면?",
    options: ["바로 해결", "시간을 둠", "감정 표현", "논리적 대화"],
  },
  {
    question: "이상적인 데이트는?",
    options: ["액티비티", "집에서 휴식", "로맨틱한 장소", "계획된 일정"],
  },
  {
    question: "연애에서 나는?",
    options: ["리더형", "배려형", "감성형", "분석형"],
  },
];

const results = {
  0: {
    type: "열정적인 탐험가 🔥",
    desc: "새로운 경험과 재미를 추구하는 연애 스타일입니다.",
    match: "안정감을 주는 현실적인 파트너",
  },
  1: {
    type: "편안한 안정형 🌿",
    desc: "편안함과 안정적인 관계를 중요하게 생각합니다.",
    match: "활력을 주는 적극적인 파트너",
  },
  2: {
    type: "감성적인 로맨티스트 💖",
    desc: "감정과 분위기를 중시하는 연애 스타일입니다.",
    match: "이해심 깊은 따뜻한 파트너",
  },
  3: {
    type: "이성적인 전략가 🧠",
    desc: "논리와 균형을 중요하게 생각하는 연애 스타일입니다.",
    match: "감정을 표현해주는 파트너",
  },
};

export default function App() {
  const [step, setStep] = useState(0);
  const [answers, setAnswers] = useState([]);

  const handleAnswer = (index) => {
    const newAnswers = [...answers, index];
    setAnswers(newAnswers);
    setStep(step + 1);
  };

  const getResult = () => {
    const sum = answers.reduce((a, b) => a + b, 0);
    return results[sum % 4];
  };

  if (step >= questions.length) {
    const result = getResult();
    return (
      <div className="min-h-screen flex flex-col items-center justify-center bg-pink-50 p-6">
        <h1 className="text-3xl font-bold mb-4">당신의 연애 스타일</h1>
        <h2 className="text-2xl mb-2">{result.type}</h2>
        <p className="mb-4">{result.desc}</p>
        <p className="font-semibold">궁합이 잘 맞는 스타일: {result.match}</p>
        <button
          className="mt-6 px-4 py-2 bg-pink-400 text-white rounded"
          onClick={() => {
            setStep(0);
            setAnswers([]);
          }}
        >
          다시 하기
        </button>
      </div>
    );
  }

  return (
    <div className="min-h-screen flex flex-col items-center justify-center bg-pink-50 p-6">
      <h1 className="text-2xl font-bold mb-6">
        {questions[step].question}
      </h1>
      <div className="grid gap-4">
        {questions[step].options.map((opt, i) => (
          <button
            key={i}
            onClick={() => handleAnswer(i)}
            className="px-6 py-3 bg-white rounded shadow hover:bg-pink-100"
          >
            {opt}
          </button>
        ))}
      </div>
    </div>
  );
}
