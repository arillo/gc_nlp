# GcNLP

Elixir wrapper for Google Cloud Natural Language API. See [Cloud Natural Language API](https://cloud.google.com/natural-language/)

Latest version 0.2.3 [doc.](https://hexdocs.pm/gc_nlp/0.2.3)

## Installation

The package can be installed as:

  1. Add `gc_nlp` to your list of dependencies in `mix.exs`:

    ```elixir
    def deps do
      [{:gc_nlp, "~> 0.2.3"}]
    end
    ```

  2. Ensure `gc_nlp` is started before your application:

    ```elixir
    def application do
      [applications: [:gc_nlp]]
    end
    ```

  3. Put your Google Cloud credential json file in 'config/' or modify the appropriate Goth config. Refer to [this guide to get your credential file.](https://cloud.google.com/natural-language/docs/common/auth) Default to expect "gcloud-secret.json" inside config directory.

## Using GcNLP

1. Sentiment Analysis

	```elixir
	iex> GcNLP.analyze_sentiment "There is a lot of new features coming in Elixir 1.4"
	%{"documentSentiment" => %{"magnitude" => 0.1, "polarity" => 1}, "language" => "en"}

	```

2. Entity Analysis

	```elixir
	iex> GcNLP.analyze_entities "There is a lot of new features coming in Elixir 1.4"
    %{"entities" => [%{"mentions" => [%{"text" => %{"beginOffset" => 41, "content" => "Elixir 1.4"}}], "metadata" => %{}, "name" => "Elixir 1.4", "salience" => 0.16144496, "type" => "OTHER"}], "language" => "en"}
	```

3. Syntactic Analysis

	```elixir
	iex> GcNLP.annotate_text "There is a lot of new features coming in Elixir 1.4"
    %{"documentSentiment" => %{"magnitude" => 0.1, "polarity" => 1}, "entities" => [%{"mentions" => [%{"text" => %{"beginOffset" => 41, "content" => "Elixir 1.4"}}], "metadata" => %{}, "name" => "Elixir 1.4", "salience" => 0.16144496, "type" => "OTHER"}], "language" => "en", "sentences" => [%{"text" => %{"beginOffset" => 0, "content" => "There is a lot of new features coming in Elixir 1.4"}}], "tokens" => [%{"dependencyEdge" => %{"headTokenIndex" => 1, "label" => "EXPL"}, "lemma" => "There", "partOfSpeech" => %{"tag" => "DET"}, "text" => %{"beginOffset" => 0, "content" => "There"}}, %{"dependencyEdge" => %{"headTokenIndex" => 1, "label" => "ROOT"}, "lemma" => "be", "partOfSpeech" => %{"tag" => "VERB"}, "text" => %{"beginOffset" => 6, "content" => "is"}}, ...}
	```

  4. Entity Sentiment Analysis

  	```elixir
    iex> GcNLP.analyze_entity_sentiment "There is a lot of new features coming in Elixir 1.6"
      %{ "entities" => [ %{ "mentions" => [ %{ "sentiment" => %{"magnitude" => 0, "score" => 0}, "text" => %{"beginOffset" => 11, "content" => "lot"}, "type" => "COMMON" } ], "metadata" => %{}, "name" => "lot", "salience" => 0.46147496, "sentiment" => %{"magnitude" => 0, "score" => 0}, "type" => "OTHER" }, %{ "mentions" => [%{ "sentiment" => %{"magnitude" => 0, "score" => 0}, "text" => %{"beginOffset" => 22, "content" => "features"}, "type" => "COMMON" } ], "metadata" => %{}, "name" => "features", "salience" => 0.36635956, "sentiment" => %{"magnitude" => 0, "score" => 0}, "type" => "OTHER" }, %{ "mentions" => [ %{ "sentiment" => %{"magnitude" => 0, "score" => 0}, "text" => %{"beginOffset" => 41, "content" => "Elixir 1.6"}, "type" => "PROPER" } ], "metadata" => %{}, "name" => "Elixir 1.6", "salience" => 0.17216548, "sentiment" => %{"magnitude" => 0, "score" => 0}, "type" => "OTHER" } ], "language" => "en"}
  	```
