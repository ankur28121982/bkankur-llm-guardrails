# bkankur

Protocol-based Responsible AI evaluation library (LLM-as-a-Judge) with pluggable judges.
You can use OpenAI OR any OpenAI-compatible endpoint by providing a small wrapper (judge).

## Install
```bash
pip install bkankur




----------------------------sample code 1------------------------------------
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

----------------------------sample code 2------------------------------------

set OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx

python -c "import os; from bkankur import BKAnkurEvaluator, Transaction; from bkankur.judges.generic import GenericOpenAIJudge; j=GenericOpenAIJudge(model='gpt-4o-mini', base_url='https://api.openai.com/v1', api_key=os.environ['OPENAI_API_KEY']); e=BKAnkurEvaluator(judge=j); tx=Transaction(user_text='How can I reset my password?', bot_text='Go to Settings → Account → Reset Password. If you forgot it, use Forgot Password on login screen.'); r=e.evaluate(tx); print(r.pretty())"

<img width="1587" height="453" alt="image" src="https://github.com/user-attachments/assets/3359218c-4497-454d-93c4-2f8bd2cec754" />
