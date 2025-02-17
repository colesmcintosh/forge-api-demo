# forge-api-demo

This is a simple demo of the Forge API by Nous Research. It demonstrates how to use the asynchronous API to trigger a reasoning completion and wait for the result.

If you want to jump straight to the code, see: [src/forge-api-demo/cli.py](https://github.com/NousResearch/forge-api-demo/blob/main/src/forge-api-demo/cli.py).

See also:
* [About Forge API](https://gist.github.com/DamascusGit/c1523fb166109aa6af81af986f856f2d)
* [API reference](https://forge-api.nousresearch.com/docs)

## Setup

Install Poetry if you don't have it:

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

Install dependencies:

```bash
poetry install
```

## Run

Here's how to run the command and see its help output:
```bash
> poetry run python src/forge-api-demo/cli.py -h
```

Which shows:
```
usage: forge-api-demo [-h] -p PROMPT [-r {fast,medium,slow}] [-t]

Simple demo of the Forge API by Nous Research. Run with env var FORGE_API_KEY set.

options:
  -h, --help            show this help message and exit
  -p PROMPT, --prompt PROMPT
                        Your prompt.
  -r {fast,medium,slow}, --reasoning-speed {fast,medium,slow}
                        The reasoning preset to use: fast/medium/slow. Defaults to medium.
  -t, --track           Whether to return detailed information about the

For more information, see: https://forge-api.nousresearch.com/docs
```

Example completion run:

```bash
FORGE_API_KEY=<YOUR_API_KEY> poetry run python src/forge-api-demo/cli.py -p "How much wood would a theoretical 80kg woodchuck chuck assuming lunar gravity and a competitive woodchucking environment?"
```

## Example outputs

### Without tracking

If I want to ask:

> How much wood would a theoretical 80kg woodchuck chuck assuming lunar gravity and a competitive woodchucking environment?

I can run the command:

```bash
> FORGE_API_KEY=<YOUR_API_KEY> poetry run python src/forge-api-demo/cli.py -p "How much wood would a theoretical 80kg woodchuck chuck assuming lunar gravity and a competitive woodchucking environment?"
```

The output includes lots of metadata but the salient piece can be found under `result.choices[0].message.content`:

```json
{
  "metadata": {
    "id": "13335ee8-7899-40ff-beac-bf8be41d0cc1",
    "config": {
      "reasoning_speed": "medium",
      "reasoning_type": "mococoa",
      "orchestrator_model": {
        "temperature": 0.7,
        "top_p": 1.0,
        "logprobs": false,
        "n": 1,
        "stop": null,
        "max_tokens": null,
        "presence_penalty": 0.0,
        "frequency_penalty": 0.0,
        "logit_bias": null,
        "modelID": "Hermes-3-70b"
      },
      "reasoning_models": [
        {
          "temperature": 0.7,
          "top_p": 1.0,
          "logprobs": false,
          "n": 1,
          "stop": null,
          "max_tokens": null,
          "presence_penalty": 0.0,
          "frequency_penalty": 0.0,
          "logit_bias": null,
          "modelID": "claude-3-5-sonnet-20241022"
        },
        {
          "temperature": 0.7,
          "top_p": 1.0,
          "logprobs": false,
          "n": 1,
          "stop": null,
          "max_tokens": null,
          "presence_penalty": 0.0,
          "frequency_penalty": 0.0,
          "logit_bias": null,
          "modelID": "gemini-1.5-pro-002"
        },
        {
          "temperature": 0.7,
          "top_p": 1.0,
          "logprobs": false,
          "n": 1,
          "stop": null,
          "max_tokens": null,
          "presence_penalty": 0.0,
          "frequency_penalty": 0.0,
          "logit_bias": null,
          "modelID": "Hermes-3-70b"
        }
      ],
      "num_simulations": 12,
      "max_depth": 10,
      "track": false,
      "logprobs": null,
      "top_logprobs": null
    },
    "status": "succeeded",
    "error": null,
    "updated_at": "2024-11-12T05:03:07.917385Z",
    "owner": "robin@nousresearch.com",
    "task_id": "76da6fe6-bf6d-432c-bbe0-af15c0eb1658",
    "progress_message": null,
    "progress": 1.0,
    "created_at": "2024-11-12T05:02:23.764050Z"
  },
  "result": {
    "id": "76da6fe6-bf6d-432c-bbe0-af15c0eb1658",
    "object": "planner.chat.completion",
    "created": 1731387787,
    "model": "Hermes-3-70b",
    "usage": {
      "prompt_tokens": 8198,
      "completion_tokens": 2606,
      "total_tokens": 10804,
      "time": 43
    },
    "choices": [
      {
        "message": {
          "content": "An 80kg woodchuck would be able to chuck approximately 581.33kg of wood on the moon in a competitive woodchucking environment. This calculation is based on the woodchuck's ability to lift its own body weight on Earth and the advantage of the lower lunar gravity (1.62 m/s² compared to Earth's 9.81 m/s²). Additionally, the competitive environment provides a 20% boost to the woodchuck's performance.",
          "role": "assistant"
        },
        "logprobs": null,
        "finish_reason": "stop",
        "index": 0
      }
    ],
    "traces": null,
    "tool_calls": null
  }
}
```

### With tracking

Tracking (`--track`) adds *very verbose* reasoning logs to the output.

```bash
> FORGE_API_KEY=<YOUR_API_KEY> poetry run python src/forge-api-demo/cli.py -p "How much wood would a theoretical 80kg woodchuck chuck assuming lunar gravity and a competitive woodchucking environment?" --track
```

```json
{
  "metadata": {
    "id": "48557f1e-b7f6-4774-b088-1c8b307aa395",
    "config": {
      "reasoning_speed": "medium",
      "reasoning_type": "mococoa",
      "orchestrator_model": {
        "temperature": 0.7,
        "top_p": 1.0,
        "logprobs": false,
        "n": 1,
        "stop": null,
        "max_tokens": null,
        "presence_penalty": 0.0,
        "frequency_penalty": 0.0,
        "logit_bias": null,
        "modelID": "Hermes-3-70b"
      },
      "reasoning_models": [
        {
          "temperature": 0.7,
          "top_p": 1.0,
          "logprobs": false,
          "n": 1,
          "stop": null,
          "max_tokens": null,
          "presence_penalty": 0.0,
          "frequency_penalty": 0.0,
          "logit_bias": null,
          "modelID": "claude-3-5-sonnet-20241022"
        },
        {
          "temperature": 0.7,
          "top_p": 1.0,
          "logprobs": false,
          "n": 1,
          "stop": null,
          "max_tokens": null,
          "presence_penalty": 0.0,
          "frequency_penalty": 0.0,
          "logit_bias": null,
          "modelID": "gemini-1.5-pro-002"
        },
        {
          "temperature": 0.7,
          "top_p": 1.0,
          "logprobs": false,
          "n": 1,
          "stop": null,
          "max_tokens": null,
          "presence_penalty": 0.0,
          "frequency_penalty": 0.0,
          "logit_bias": null,
          "modelID": "Hermes-3-70b"
        }
      ],
      "num_simulations": 12,
      "max_depth": 10,
      "track": true,
      "logprobs": null,
      "top_logprobs": null
    },
    "status": "succeeded",
    "error": null,
    "updated_at": "2024-11-12T04:59:35.387598Z",
    "owner": "robin@nousresearch.com",
    "task_id": "0f9ed8a0-0d36-4f53-bd3a-610f19804385",
    "progress_message": null,
    "progress": 1.0,
    "created_at": "2024-11-12T04:58:52.792813Z"
  },
  "result": {
    "id": "0f9ed8a0-0d36-4f53-bd3a-610f19804385",
    "object": "planner.chat.completion",
    "created": 1731387575,
    "model": "Hermes-3-70b",
    "usage": {
      "prompt_tokens": 8274,
      "completion_tokens": 2058,
      "total_tokens": 10332,
      "time": 42
    },
    "choices": [
      {
        "message": {
          "content": "In a competitive woodchucking environment on the moon, an 80kg woodchuck would be able to chuck approximately 387.56kg of wood. This calculation takes into account the difference in gravity between Earth and the moon, as well as a fatigue factor due to the space environment. The reduced gravity on the moon provides a mechanical advantage, allowing the woodchuck to chuck more wood than it would on Earth.",
          "role": "assistant"
        },
        "logprobs": null,
        "finish_reason": "stop",
        "index": 0
      }
    ],
    "traces": {
      "nodes": [
        // ... (traces omitted for brevity)
      ]
    }
  }
}
```

## License

This project is licensed under the MIT License.
