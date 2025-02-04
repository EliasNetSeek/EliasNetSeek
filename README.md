```elixir
defmodule Dev do
  defstruct name: "Elias",
            role: "Software Engineer",
            speak: %{"ro-RO" => "Romanian", "en-US" => "English"},
            exp: ["Web Developer", "Web Designer", "Software Integrator", "DevOps Engineer"],
            skills: ["JavaScript", "Python", "C#", "Django", "Flask"]
end

defmodule GenerateReadme do
  def generate_readme(%Dev{name: name, role: role, exp: exp, speak: speak, skills: skills}) do
    [
      "# Hello world! :wave: My name is #{name}.",
      "I'm a #{role} with #{format_list(exp)} background.",
      "I speak #{format_list(Map.values(speak))}.\n",
      "## :rocket: My Tech Stack:\n```\n#{Enum.join(skills, ", ")}\n```",
      "Let's connect and build amazing things together! :wink:"
    ]
    |> Enum.join("\n")
  end

  defp format_list([single]), do: single
  defp format_list(list) do
    Enum.split(list, -1)
    |> (fn {rest, [last]} -> Enum.join(rest, ", ") <> ", and " <> last end).()
  end

  def run do
    me = %Dev{}
    IO.puts(generate_readme(me))
  end
end
```
