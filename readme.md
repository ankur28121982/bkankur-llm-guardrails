# bkankur

Protocol-based Responsible AI evaluation library (LLM-as-a-Judge) with pluggable judges.
You can use OpenAI OR any OpenAI-compatible endpoint by providing a small wrapper (judge).

## Install
```bash
pip install bkankur




----------------------------sample code------------------------------------
import os
from bkankur import BKAnkurEvaluator, Transaction
from bkankur.judges.generic import GenericOpenAIJudge

judge = GenericOpenAIJudge(
    model="gpt-4o-mini",
    base_url="https://api.openai.com/v1",
    api_key=os.getenv("OPENAI_API_KEY"),
    timeout_s=60,
)

evaluator = BKAnkurEvaluator(judge=judge)

tx = Transaction(
    user_text="I feel anxious",
    bot_text="Try box breathing: inhale 4, hold 4, exhale 4. Seek help if severe."
)

report = evaluator.evaluate(tx)
print(report.pretty())
