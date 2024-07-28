# MethodsForSeleniumOnJava
Methods for selenium on java

~~~java

	public static String obtenerValorTd(String html, String tableId, String tdId) {

		String[] trs = encontrarPrimerosDosTr(html, tableId);

		if (!trs[0].startsWith("No se encontró")) {

			String tdContent = encontrarTdPorId(trs[0], tdId);

			if (tdContent.startsWith("No se encontró")) {

				if (!trs[1].startsWith("No se encontró")) {

					tdContent = encontrarTdPorId(trs[1], tdId);

				}

			}

			return tdContent;

		}

		else {

			return trs[0];

		}

	}

	public static String encontrarTdPorId(String trContent, String tdId) {

		String tdPatternString = "<td[^>]*\\bid\\s*=\\s*['\"]" + tdId + "['\"][^>]*>";

		Pattern tdPattern = Pattern.compile(tdPatternString, Pattern.CASE_INSENSITIVE);

		Matcher tdMatcher = tdPattern.matcher(trContent);

		if (!tdMatcher.find()) {

			return "No se encontró el <td> con el id '" + tdId + "' en el <tr>.";

		}

		int tdStartIndex = tdMatcher.end();

		int tdEndIndex = trContent.indexOf("</td>", tdStartIndex);

		if (tdEndIndex == -1) {

			return "No se encontró el final del <td> con el id '" + tdId + "'.";

		}

		return trContent.substring(tdStartIndex, tdEndIndex).trim();

	}

	public static void addCookiesToDriver(WebDriver driver, HashMap<String, String> cookies) {

    for (Map.Entry<String, String> entry : cookies.entrySet()) {

			Cookie cookie = new Cookie(entry.getKey(), entry.getValue());

			driver.manage().addCookie(cookie);

    }

  }

	public static void ponerValorSelect(WebDriver driver, String selectId, String value) {

		try {

			WebElement selectElement = driver.findElement(By.id(selectId));

			Select select = new Select(selectElement);

			java.util.List<WebElement> options = selectElement.findElements(By.tagName("option"));

			if (!options.isEmpty()) {

				select.selectByValue(value);

			}

		}

		catch (Exception e) {

		}

	}

~~~
