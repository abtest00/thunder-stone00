# Notes

- Separate three constructs in every comparison: the task/eval corpus, the context or skill version, and the runtime (model, tools, permissions, configuration). Changing more than one makes the result non-attributable.
- Retrieval metrics alone—such as whether a document was retrieved—are diagnostic signals, not proof that the supplied context improved the final task outcome.
- For knowledge-graph context, score provenance/effective-date use and the ability to say “insufficient evidence,” not just answer fluency.
- For skills, activation and non-activation are both product behavior. A skill that fires for nearby unrelated tasks is a regression even if its output is good when explicitly invoked.
- Automated judges need calibration against blinded human labels before being used as a regression gate. Watch for verbosity and position bias.
- The OpenAI Evals platform has a stated deprecation timeline in current documentation; the recommended durable design here is therefore tool-agnostic: versioned dataset + captured runs/artifacts + explicit graders/rubrics.
