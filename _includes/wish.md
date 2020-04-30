{% capture newline %}
{% endcapture %}

{% capture row_id %}row{% increment wish_counter %}{% endcapture %}

<tr style="page-break-inside:avoid" id="{{row_id}}">
<td class="noborder no-print"><input type="checkbox" checked onchange="document.getElementById('{{row_id}}').classList.toggle('no-print')"></td>

<td markdown="1" class="fitwidth noborder">

{% assign total_shots = 0 %}
{% assign lines = include.wish | split: newline -%}
{% for line in lines %}
{% assign symbols = line | split: " " %}{% for symbol in symbols -%}
{%- assign total_shots = total_shots | plus: symbol -%}
| {% if symbol == "0" %}&nbsp;{% else %}{{ symbol }}{% endif %} {% endfor %}
{%- endfor %}
{:.wish-table}

</td>
<td markdown="1" class="fitwidth noborder">

{% for line in lines %}
{% assign symbols = line | split: " " %}{% for symbol in symbols -%}
| {% if symbol == "0" %}&nbsp;{% else %}<img src="/assets/img/last_wish_symbol{{ symbol }}.png">{% endif %} {% endfor %}
{%- endfor %}
{:.wish-table}

</td>
<td markdown="1" class="stretch noborder">

{{ include.description | newline_to_br }}<br />
Total shots required: {{ total_shots }}
{: style="width: 100%"}

</td>
</tr>
