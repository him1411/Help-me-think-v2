# Help-Me-Think-v2.0

This repository maintains a community effort to create large collection of tasks which needs customization, thinking or expertise (i.e., hard for average humans to do). 
We welcome external collaboration or suggestions to make this dataset better and bigger! 🙌  
We invite submission of new tasks to this benchmark by way of [GitHub pull request](https://github.com/allenai/natural-instructions-expansion/pulls), through **October 30, 2022**. 
The contributors with meaningful contribution to our tasks will be included as co-authors on a paper that will announce the benchmark as well as analysis/results on it.

## Background

This collection of tasks is the extension of the work done in [HELP ME THINK - v1.0](https://arxiv.org/pdf/2208.08232.pdf).

### Objective

**TLDR**; Controlling the text generated by language models and customizing the content has been a long-standing challenge. Existing prompting techniques proposed in pursuit of providing control are task-specific and lack generality; this provides overwhelming choices for non-expert users to find a suitable method for their task. The effort associated with those techniques, such as in writing examples, explanations, instructions, etc. further limits their adoption among non-expert users. To allivate this issue, we propose [HELP ME THINK](https://arxiv.org/pdf/2208.08232.pdf) prompting technique which allows non-expert user to use Large Language Models (LLMs) like GPT-3 s by asking a set of relevant questions and leveraging user answers to execute the task.

### Any empirical evidence that this might be true?

Our [recent study](https://arxiv.org/pdf/2208.08232.pdf) shows (across 63 tasks) that this prompting technique is effective in performing tasks that requires expert human knowledge or customization.

### What do we mean by "meaningful contribution"? 
If you're among top `k` [contributors](https://github.com/allenai/natural-instructions-expansion/graphs/contributors) (say, `k=25`), or if you have contributed at least `25` tasks and help us in evaluating `25` tasks. Depending on the overall contributions, we will adjust these constants so that the number of authors don't exeed `m` (say, `m=35`). 

## How to Create a Task?

Let's create a task for generating a bio for you.

**Step 1**: You need to start with pre_question_prompt which helps you to generate the question-answer pairs.

pre_question_prompt: `I am an expert $task-executer$. I will ask some questions to collect information and then I will use the information to $do the task.$`

Here, you can replace `$task-executer$` and `$do the task.$` with actual task. Now, let's write this prompt for bio task: `I am an expert bio generator. I will ask some questions to collect information and then I will use the information to write a bio for you.`

**Step 2**: Now GPT-3 will start generating Question-Answer (QA) pairs for you. You can customize GPT-3 generated answers if you want.

**Step 3**: Once you collect all QA pairs, use task specific prompt -

`Write a $task-specific-output$ using the questions and answers above. $task-specific-instruction$`

Here, replace `$task-specific-output$` with actual task and also you can add extra instructions if you want at place of `$task-specific-instruction$`. Now, let's write a this prompt for bio task - `Write a bio for me using the questions and answers above. Write a short bio.`

**Step 4**: For the same task, generate 3 instances by changing the answers, accordingly, GPT3 might generate different questions.

**Step 5**: Save preset link for each instance.

**Step 5**: Once you have all this, generate `.json` file as below and submit pull request.

```python
{
  "Contributor": "",
  "Domain": "",
  "Task": "",
  "Prompt": {"pre_question_prompt": "", "task_specific_prompt": ""},
  "Instances": [
    {"QApair": [{"Question": "", "Answer": ""}, {"Question": "", "Answer": ""}, ...], "Output": ""},
    {"QApair": [{"Question": "", "Answer": ""}, {"Question": "", "Answer": ""}, ...], "Output": ""},
    {"QApair": [{"Question": "", "Answer": ""}, {"Question": "", "Answer": ""}, ...], "Output": ""},
  ],
  "Preset_link": ["", "", ""]
}
```

## How to Contribute

We would appreciate any external contributions! 🙏

 * All submissions must be submitted via [Github pull requests](https://github.com/allenai/natural-instructions-expansion/pulls). These submissions will undergo a review before being merged. 
 * Each task must contain contain a `.json` file that contains the task content and follow task schema. You can look inside the [`tasks/`](tasks) directory for several examples.  
    * Make sure that your json is human readable (use proper indentation; e.g., in Python: `json.dumps(your_json_string, indent=4, ensure_ascii=False)`)   
    * Make sure that you json file is not bigger than 50MB. 
    * Make sure your task has no more 3 instances.
    * Make sure to number your task json correctly (Look at the task number in the latest pull request, task number in your submission should be the next number).
    * Make sure to create a pull request after creating all possible tasks. You can have one pull request with multiple tasks.
 * Add your task to [our list of tasks](tasks/README.md).
 * To make sure that your addition is formatted correctly, tests will automatically run at the timne of pull request: `> python src/test_all.py`
 * The pull request will be merged only if all test cases will be passed.
  
 
If you have any questions or suggestions, please use [the issues](https://github.com/allenai/natural-instructions-expansion/issues) feature.
